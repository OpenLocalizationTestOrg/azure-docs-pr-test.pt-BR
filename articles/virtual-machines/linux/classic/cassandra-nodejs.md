---
title: aaaRun Cassandra com Linux no Azure | Microsoft Docs
description: "Como toorun um Cassandra cluster no Linux em máquinas virtuais do Azure de um aplicativo Node. js"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Executando Cassandra com Linux no Azure e acessando-a do Node.js
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Consulte modelos do Resource Manager para [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) e [Cluster Spark e Cassandra CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Visão geral
O Microsoft Azure é uma plataforma de nuvem aberta que executa tanto os softwares da Microsoft quanto os não pertencentes à Microsoft, que inclui sistemas operacionais, servidores de aplicativos, middlewares de mensagens, bem como bancos de dados SQL e NoSQL de ambos os modelos de software livre e comercial. A criação de serviços resilientes em nuvens públicas, incluindo o Azure, requer um planejamento cuidadoso e uma arquitetura deliberada para ambos os servidores de aplicativos, bem como camadas de armazenamento. A arquitetura de armazenamento distribuída de Cassandra naturalmente ajuda na criação de sistemas altamente disponíveis que são tolerantes a falhas para as falhas de cluster. Cassandra é um banco de dados NoSQL de escala na nuvem mantido pela Apache Software Foundation em cassandra.apache.org; Cassandra é escrito em Java e, portanto, pode ser executado em ambas as plataformas Windows e Linux.

foco Olá deste artigo é implantação de Cassandra tooshow no Ubuntu como um cluster único e vários data center utilizando máquinas virtuais do Microsoft Azure e redes virtuais. Hello implantação de cluster para cargas de trabalho de produção otimização está fora do escopo deste artigo conforme ele requer a configuração de nó em vários discos, Olá toosupport de modelagem de dados e de design da topologia de anel apropriado necessário replicação, a consistência dos dados, a taxa de transferência e requisitos de alta disponibilidade.

Essa demora artigo tooshow uma abordagem fundamental que o que está envolvido na criação Olá cluster Cassandra em comparação com Docker, Chef ou Puppet que pode tornar Olá muito mais fácil de implantação de infraestrutura.  

## <a name="hello-deployment-models"></a>Olá modelos de implantação
Rede do Microsoft Azure permite que a implantação Olá de clusters privadas isolados, acesso de saudação do qual pode ser restrito tooattain fina rede refinada segurança.  Como este artigo é sobre a implantação de Cassandra Olá em um nível fundamental de exibição, nos concentraremos não em nível de consistência hello e design de armazenamento ideal de saudação para taxa de transferência. Aqui está a lista de saudação de requisitos de rede para nosso cluster hipotético:

* Os sistemas externos não podem acessar o banco de dados de Cassandra desde dentro ou fora do Azure
* Cluster Cassandra tem toobe atrás de um balanceador de carga para tráfego thrift
* Implantar nós de Cassandra em dois grupos em cada data center para uma disponibilidade de cluster aprimorada
* Bloquear o cluster Olá assim que somente o farm de servidores de aplicativo tem o banco de dados do access toohello diretamente
* Nenhum ponto de extremidade de rede pública diferente de SSH
* Cada nó de Cassandra precisa de um endereço IP interno fixo

Cassandra pode ser implantado tooa única região do Azure ou regiões toomultiple com base na natureza Olá distribuída de carga de trabalho de saudação. Modelo de implantação de várias regiões pode ser utilizado tooserve os usuários finais mais tooa específico geografia por meio de saudação mesma infraestrutura Cassandra. Nó interno replicação cuida do Cassandra da sincronização de saudação de vários mestres grava provenientes de vários data centers e apresenta uma exibição consistente de saudação tooapplications de dados. Implantação de várias regiões também pode ajudar com a redução de riscos de saudação de interrupções de serviço do Azure mais ampla hello. A consistência ajustável e a replicação de topologia de Cassandra ajudará a atender às diversas necessidades de RPO dos aplicativos.

### <a name="single-region-deployment"></a>Implantação de região única
Vamos começar com uma implantação de região única e coleta Olá conhecimentos na criação de um modelo de várias regiões. Rede virtual do Azure será usado toocreate isolada sub-redes para que os requisitos de segurança de rede Olá mencionados acima podem ser atendidos.  processo de saudação descrito na criação de implantação de região única Olá usa Ubuntu 14.04 LTS e Cassandra 2.08; No entanto, o processo de saudação pode facilmente ser adotada toohello outras variantes do Linux. Olá seguem algumas das características de saudação sistemático de implantação de região única hello.  

**Alta disponibilidade:** Olá nós Cassandra mostradas Olá Figura 1 são implantados conjuntos de disponibilidade de tootwo para que nós Olá são distribuídos entre vários domínios de falha para alta disponibilidade. VMs anotadas com cada conjunto de disponibilidade é mapeada too2 domínios de falha.  Microsoft Azure usa Olá conceito de toomanage de domínio de falhas não planejada para baixo de tempo (por exemplo, falhas de hardware ou software) ao conceito de saudação do domínio de atualização (por exemplo, o host ou convidado patches/atualizações do SO, atualizações de aplicativo) é usado para gerenciar agendado tempo de inatividade. Consulte [recuperação de desastres e alta disponibilidade para aplicativos do Azure](http://msdn.microsoft.com/library/dn251004.aspx) para a função hello de domínios de falha e atualização na obtenção de alta disponibilidade.

![Implantação de região única](./media/cassandra-nodejs/cassandra-linux1.png)

Figura 1: implantação de região única

Observe que, no tempo de saudação da redação deste artigo, Azure não permite mapeamento explícito de saudação de um grupo de domínio de falha específico de tooa de VMs; Portanto, mesmo com o modelo de implantação Olá mostrado na Figura 1, é estatisticamente provável que todas as máquinas virtuais de saudação pode ser mapeado tootwo domínios de falha em vez de quatro.

**O balanceamento de carga do tráfego Thrift:** bibliotecas de cliente Thrift dentro do servidor de web hello conectar toohello cluster por meio de um balanceador de carga interno. Isso requer que o processo de saudação de adicionar sub-rede de saudação de carga interno balanceador toohello "dados" (consulte a Figura 1) no contexto de Olá Olá do serviço de nuvem hospeda Olá Cassandra cluster. Depois que o balanceador de carga interno Olá for definida, cada nó requer toobe de ponto de extremidade com balanceamento de carga Olá adicionado com anotações de saudação de um conjunto com balanceamento de carga com anteriormente nome do balanceador de carga definido. Confira [Balanceamento de carga interno do Azure ](../../../load-balancer/load-balancer-internal-overview.md)para obter mais detalhes.

**Sementes de cluster:** é importante tooselect Olá a maioria de nós de alta disponibilidade para sementes como Olá novos nós se comunicará com topologia de saudação de toodiscover semente nós de cluster de saudação. Um nó de cada conjunto de disponibilidade é designado como semente nós tooavoid único ponto de falha.

**Fator de replicação e o nível de consistência:** compilação em alta disponibilidade durabilidade de dados e da Cassandra é caracterizada por Olá fator de replicação (FR - número de cópias de cada linha armazenada no cluster de saudação) e (número de nível de consistência réplicas toobe lida/gravada antes de retornar o chamador de toohello resultados Olá). Fator de replicação é especificado durante a saudação criação KEYSPACE (banco de dados relacional de semelhante tooa) enquanto o nível de consistência de saudação for especificado ao emitir consultas CRUD hello. Consulte a documentação de Cassandra em [configurando para consistência](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes de consistência e a fórmula Olá para a computação de quorum.

Cassandra dá suporte a dois tipos de modelos de integridade de dados – consistência e consistência Eventual. Olá fator de replicação e o nível de consistência juntos determinará se dados saudação será consistentes assim que uma operação de gravação é concluída ou é finalmente consistente. Por exemplo, QUORUM (por exemplo, um) especificando o QUORUM como Olá que nível de consistência será sempre garante a consistência de dados durante qualquer nível de consistência, abaixo do número de saudação de réplicas toobe gravado como tooattain necessário resulta em dados sendo finalmente consistente.

mostrado acima, com um fator de replicação de 3 e QUORUM de cluster de 8 nós Hello (2 nós são lidos ou gravados para consistência) nível de consistência de leitura/gravação, pode sobreviver a perda de teórico Olá de em Olá 1 nó por replicação de grupo antes de iniciar o aplicativo hello Perceba a falha de saudação. Isso pressupõe que todos os espaços de chave Olá também tem balanceamento de solicitações de leitura/gravação.  Olá seguem parâmetros Olá que usaremos para cluster Olá implantado:

Configuração de cluster de Cassandra de região única:

| Parâmetros de cluster | Valor | Comentários |
| --- | --- | --- |
| Número de nós (N) |8 |Número total de nós no cluster Olá |
| Fator de replicação (RF) |3 |Número de réplicas de uma determinada linha |
| Nível de consistência (gravação) |QUORUM[(RF/2) +1) = 2] Olá resultado de saudação fórmula é arredondada para baixo |Grava no hello mais 2 réplicas antes de resposta de saudação é enviada do chamador toohello 3º réplica é gravada de forma consistente eventualmente. |
| Nível de consistência (leitura) |QUORUM [(RF/2) + 1 = 2] resultado de saudação da fórmula Olá será arredondado para baixo |Lê 2 réplicas antes de enviar o chamador de toohello de resposta. |
| Estratégia de replicação |NetworkTopologyStrategy consulte [Replicação de dados](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) na documentação de Cassandra para obter mais informações |Compreende a topologia de implantação hello e coloca réplicas em nós para que todas as réplicas de saudação não terminem em Olá mesmo rack |
| Informante |GossipingPropertyFileSnitch consulte [Informantes](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) na documentação de Cassandra para obter mais informações |NetworkTopologyStrategy usa um conceito de topologia de saudação do snitch toounderstand. GossipingPropertyFileSnitch fornece melhor controle no mapeamento cada centro do nó toodata e rack. cluster Hello, em seguida, usa fofocas toopropagate essas informações. Isso é muito mais simples no dinâmico tooPropertyFileSnitch relativo de configuração de IP |

**Considerações do azure para o cluster do Cassandra:** o recurso de máquinas virtuais do Microsoft Azure usa o armazenamento de Blob do Azure para persistência de disco; o Armazenamento do Azure salva 3 réplicas de cada disco para alta durabilidade. Isso significa que cada linha de dados inseridos em uma tabela de Cassandra já esteja armazenada em 3 réplicas e, portanto, a consistência dos dados é já resolvida mesmo se Olá fator de replicação (FR) é 1. Olá problema principal fator de replicação sendo 1 é que o aplicativo hello terá tempo de inatividade mesmo se um único nó Cassandra falha. No entanto, se um nó estiver inativo para problemas de saudação (por exemplo, o hardware, falhas de software do sistema) reconhecidos pelo controlador de malha do Azure, ele provisionará um novo nó no seu local usando Olá mesmo unidades de armazenamento. O provisionamento de um novo nó tooreplace Olá antigo um pode levar alguns minutos.  Da mesma forma para atividades de manutenção planejada, como alterações de sistema operacional convidado, Cassandra atualizações e alterações de aplicativo, controlador de malha do Azure executa atualizações de nós Olá contínuas em cluster hello.  Atualizações sem interrupção também podem desativar alguns nós em um momento e, portanto, o cluster Olá pode experimentar breve tempo de inatividade para algumas partições. No entanto, os dados de saudação não serão perdidos devido a redundância de armazenamento do Azure interna toohello.  

Para sistemas implantados tooAzure que não exige uma alta disponibilidade (por exemplo, 99,9 em torno que é equivalente too8.76 h/ano; consulte [alta disponibilidade](http://en.wikipedia.org/wiki/High_availability) para obter detalhes) pode ser capaz de toorun com RF = 1 e nível de consistência = um.  Para aplicativos com requisitos de alta disponibilidade, RF = 3 e nível de consistência = QUORUM será tolerar Olá tempo de inatividade do que um de nós de saudação uma das réplicas de saudação. RF = 1 em implantações tradicionais (por exemplo, no local) não pode ser usado devido toohello possível perda de dados resultantes de problemas, como falhas no disco.   

## <a name="multi-region-deployment"></a>Implantação em várias regiões
Da Cassandra replicação com reconhecimento de centro de dados e modelo de consistência descrito acima ajuda com a implantação de várias regiões Olá imediato saudação sem Olá necessário para qualquer ferramentas externas. Isso é bastante diferente do hello relacional bancos de dados tradicionais onde a instalação Olá para espelhamento de banco de dados para gravações de vários mestres pode ser bastante complexa. Cassandra em uma multi-região de configurar pode ajudar em cenários de uso de saudação incluindo Olá seguinte:

**Implantação baseada em proximidade:** aplicativos multilocatários, com Limpar mapeamento de usuários de locatário-para-região, pode ser se beneficiam por latências de baixa do cluster de várias regiões hello. Por exemplo, um gerenciamento de aprendizado de sistemas para instituições educacionais podem implantar um cluster distribuído no Leste dos EUA e Oeste dos EUA regiões tooserve Olá respectivas áreas para transacional, bem como a análise. dados de saudação podem ser localmente consistentes em Olá tempo leituras e gravações e podem ser finalmente consistentes entre as duas regiões hello. Existem outros exemplos, como distribuição de mídia, comércio eletrônico e qualquer coisa que sirva à base de usuários concentrada geograficamente é um bom caso de uso esse modelo de implantação.

**Alta disponibilidade:** a redundância é um fator importante na obtenção de alta disponibilidade de software e hardware; confira Criando sistemas de nuvem confiáveis no Microsoft Azure para obter detalhes. No Microsoft Azure, Olá único modo seguro de obter redundância real é implantando um cluster de várias regiões. Aplicativos podem ser implantados em um modo ativo-ativo ou ativo-passivo e se uma das regiões Olá estiver inativo, o Azure Traffic Manager pode redirecionar região ativa do tráfego toohello.  Com a implantação de região única Olá, se a disponibilidade de saudação for 99,9, uma implantação de duas regiões pode atingir uma disponibilidade de 99,9999 calculado pela fórmula Olá: (1-(1-0.999) * (1-0,999)) * 100); Consulte Olá acima papel para obter detalhes.

**Recuperação de desastres:** o cluster Cassandra de várias regiões, se projetado adequadamente, pode resistir a interrupções catastróficas do data center. Se uma região estiver inativo, Olá aplicativo implantado tooother regiões podem iniciar atendendo os usuários finais de saudação. Como as outras implementações de continuidade de negócios, o aplicativo hello tem toobe tolerante a falhas para alguma perda de dados resultante de dados de saudação no pipeline assíncrono hello. No entanto, Cassandra torna a recuperação de saudação muito swifter do tempo de saudação usado por processos de recuperação de banco de dados tradicional. A Figura 2 mostra o modelo de implantação de várias regiões típica Olá com oito nós em cada região. Ambas as regiões são imagens de espelhamento da outra para hello mesmo de simetria; designs de reais dependem do tipo de carga de trabalho da saudação (por exemplo, transacional ou analítico), o RPO, RTO, consistência dos dados e requisitos de disponibilidade.

![Implantação de várias regiões](./media/cassandra-nodejs/cassandra-linux2.png)

Figura 2: implantação do Cassandra de várias regiões

### <a name="network-integration"></a>Integração de rede
Conjuntos de máquinas virtuais tooprivate implantado redes localizados em duas regiões comunica-se entre si usando um túnel VPN. túnel VPN Olá conecta dois gateways software provisionados durante o processo de implantação de rede de saudação. Ambas as regiões têm arquitetura semelhante de rede em termos de sub-redes "web" e "dados"; Rede do Azure permite a criação de saudação de sub-redes tantos conforme necessário e aplique as ACLs conforme necessário para segurança de rede. Ao projetar a topologia de cluster Olá inter dados center comunicação latência e hello econômico impacto do tráfego de rede de saudação necessidade toobe considerado.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Consistência de dados para implantação em vários data centers
Distribuído implantações necessidade toobe atento ao impacto de topologia de cluster de saudação na taxa de transferência e a alta disponibilidade. Olá RF e nível de consistência toobe necessidade selecionada de forma que Olá quorum não depende de disponibilidade de saudação de todos os centros de dados de saudação.
Para um sistema que precisa de consistência alta, um LOCAL_QUORUM para nível de consistência (para leituras e gravações) garantirá que Olá local leituras e gravações são atendidas Olá local nós enquanto os dados são replicados de forma assíncrona toohello centros de dados remotos.  A tabela 2 resume configuração Olá detalhes para o cluster de várias regiões Olá descritas Olá gravação.

**Configuração de cluster Cassandra de duas regiões**

| Parâmetros de cluster | Valor | Comentários |
| --- | --- | --- |
| Número de nós (N) |8 + 8 |Número total de nós no cluster Olá |
| Fator de replicação (RF) |3 |Número de réplicas de uma determinada linha |
| Nível de consistência (gravação) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] resultado de saudação da fórmula Olá será arredondado para baixo |2 nós serão gravados toohello primeiro centro de dados de forma síncrona; Olá adicionais 2 nós necessários para quorum serão gravados assincronamente toohello 2º data centers. |
| Nível de consistência (leitura) |LOCAL_QUORUM ((RF/2) + 1) = 2 resultado de saudação da fórmula Olá será arredondado para baixo |Solicitações de leitura são atendidas apenas uma região. 2 nós são lidas antes do envio back toohello cliente de resposta de saudação. |
| Estratégia de replicação |NetworkTopologyStrategy consulte [Replicação de dados](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) na documentação de Cassandra para obter mais informações |Compreende a topologia de implantação hello e coloca réplicas em nós para que todas as réplicas de saudação não terminem em Olá mesmo rack |
| Informante |GossipingPropertyFileSnitch consulte [Informantes](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) na documentação de Cassandra para obter mais informações |NetworkTopologyStrategy usa um conceito de topologia de saudação do snitch toounderstand. GossipingPropertyFileSnitch fornece melhor controle no mapeamento cada centro do nó toodata e rack. cluster Hello, em seguida, usa fofocas toopropagate essas informações. Isso é muito mais simples no dinâmico tooPropertyFileSnitch relativo de configuração de IP |

## <a name="hello-software-configuration"></a>Olá a configuração de SOFTWARE
Olá versões de software a seguir é usada durante a implantação de saudação:

<table>
<tr><th>Software</th><th>Fonte</th><th>Versão</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Como fazer o download do JRE requer aceitação manual de licença do Oracle, implantação de saudação toosimplify, download que todos Olá área de trabalho de toohello de software necessárias para carregar mais tarde na imagem de modelo Ubuntu Olá que estamos criando como um cluster de toohello precursor implantação.

Baixe Olá acima de software em um diretório de download conhecidas (por exemplo, %TEMP%/downloads no Windows ou ~/Downloads na maioria das distribuições do Linux ou Mac) no computador local hello.

### <a name="create-ubuntu-vm"></a>CRIAR UMA MV UBUNTU
Nesta etapa do processo de saudação criaremos Ubuntu imagem com o software de pré-requisito Olá para que hello imagem pode ser reutilizada para o provisionamento de vários nós Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>ETAPA 1: gerar o par de chave SSH
Azure precisa de uma chave pública de PEM ou DER codificado a saudação tempo de provisionamento de X509. Gerar um par de chaves pública/privada usando instruções Olá localizadas como tooUse SSH com Linux no Azure. Se você planejar toouse putty.exe como um cliente SSH no Windows ou Linux, você terá tooconvert Olá PEM codificada em formato de tooPPK de chave privada do RSA usando puttygen.exe; instruções de saudação para isso podem ser encontradas no hello acima da página da web.

#### <a name="step-2-create-ubuntu-template-vm"></a>ETAPA 2: criar uma VM do modelo Ubuntu
modelo de saudação toocreate VM, faça logon no hello Azure clássico Olá portal e use sequência a seguir: clique em novo, computação, máquina VIRTUAL, da GALERIA, UBUNTU, Ubuntu Server 14.04 LTS e, em seguida, clique na seta direita hello. Para obter um tutorial que descreve como toocreate uma VM do Linux, consulte Criar uma máquina Virtual executando o Linux.

Digite hello segue as informações na tela hello "configuração de máquina Virtual" #1:

<table>
<tr><th>NOME DO CAMPO              </td><td>       VALOR DO CAMPO               </td><td>         COMENTÁRIOS                </td><tr>
<tr><td>DATA DE LANÇAMENTO DA VERSÃO    </td><td> Selecione uma data de saudação da lista suspensa</td><td></td><tr>
<tr><td>NOME DA MÁQUINA VIRTUAL    </td><td> cass-template                   </td><td> Este é o nome de host de saudação do hello VM </td><tr>
<tr><td>CAMADA                     </td><td> STANDARD                           </td><td> Deixe o padrão de saudação              </td><tr>
<tr><td>TAMANHO adequado                     </td><td> A1                              </td><td>Selecione Olá que VM com base em hello e/s necessidades. para essa finalidade deixe o padrão de saudação </td><tr>
<tr><td> NOVO NOME DE USUÁRIO             </td><td> localadmin                       </td><td> "admin" é um nome de usuário reservado no Ubuntu 12.xx e depois</td><tr>
<tr><td> AUTENTICAÇÃO         </td><td> Clique na caixa de seleção                 </td><td>Verifique se você quiser toosecure com uma chave SSH </td><tr>
<tr><td> CERTIFICADO             </td><td> nome do arquivo do certificado de chave pública Olá </td><td> Usar chave pública de saudação gerado anteriormente</td><tr>
<tr><td> Nova senha    </td><td> senha de alta segurança </td><td> </td><tr>
<tr><td> Confirmar Senha    </td><td> senha de alta segurança </td><td></td><tr>
</table>

Digite hello segue as informações na tela hello "configuração de máquina Virtual" #2:

<table>
<tr><th>NOME DO CAMPO             </th><th> VALOR DO CAMPO                       </th><th> COMENTÁRIOS                                 </th></tr>
<tr><td> SERVIÇO DE NUVEM    </td><td> Crie um novo serviço de nuvem    </td><td>O serviço de nuvem é um recurso de contêiner de computação, como as máquinas virtuais</td></tr>
<tr><td> NOME DNS DO SERVIÇO DE NUVEM    </td><td>ubuntu-template.cloudapp.net    </td><td>Dê um nome do balanceador de carga independente da máquina</td></tr>
<tr><td> REGIÃO/GRUPO DE AFINIDADE/REDE VIRTUAL </td><td>    Oeste dos EUA    </td><td> Selecione uma região na qual seus aplicativos web acessam cluster de Cassandra Olá</td></tr>
<tr><td>CONTA DE ARMAZENAMENTO </td><td>    Usar padrão    </td><td>Usar conta de armazenamento saudação padrão ou uma conta de armazenamento previamente criado em uma determinada região</td></tr>
<tr><td>Conjunto de disponibilidade </td><td>    Nenhum </td><td>    Deixe em branco</td></tr>
<tr><td>PONTOS DE EXTREMIDADE    </td><td>Usar padrão </td><td>    Usar configuração de SSH saudação padrão </td></tr>
</table>

Clique na seta para direita, mantenha os padrões de saudação na tela hello #3 e clique em hello "Verificar" botão toocomplete Olá VM processo de provisionamento. Depois de alguns minutos, Olá VM com hello "ubuntu-modelo de nome" deve estar em um status "em execução".

### <a name="install-hello-necessary-software"></a>INSTALAR Olá SOFTWARE necessário
#### <a name="step-1-upload-tarballs"></a>ETAPA 1: carregar tarballs
Usando o scp ou pscp, Olá cópia baixados anteriormente software muito ~ / diretório de downloads usando Olá formato de comando a seguir:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Repita Olá acima comando para JRE bem como para bits de Cassandra hello.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>Etapa 2: Preparar a estrutura de diretórios hello e extrair arquivos Olá
Faça logon no hello VM e criar a estrutura de diretórios hello e extrair o software como um superusuário com hello bash script abaixo:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Se você colar esse script na janela vim, fazer o carro de saudação tooremove se retornar ('\r ") usando o comando a seguir de saudação:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Etapa 3: editar etc/profile
Acrescente o seguinte Olá final hello:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Etapa 4: instalar JNA para sistemas de produção
Sequência de comando a seguir de saudação de uso: comando a seguir Olá jna install-3.2.7.jar e jna de plataforma de 3.2.7.jar too/usr/share.java diretório sudo apt get instalará libjna java

Crie links simbólicos no diretório $CASS_HOME/lib para que o script de inicialização de Cassandra possa encontrar essas jars:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Etapa 5: configurar o cassandra.yaml
Edite cassandra.yaml em cada configuração da VM tooreflect necessária para todas as máquinas virtuais de saudação [nós serão ajustar isso durante o provisionamento real de saudação]:

<table>
<tr><th>Nome do campo   </th><th> Valor  </th><th>    Comentários </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> Use o nome de saudação que reflete a implantação</td></tr>
<tr><td>listen_address    </td><td>[deixe em branco]    </td><td> Excluir "localhost" </td></tr>
<tr><td>rpc_addres   </td><td>[deixe em branco]    </td><td> Excluir "localhost" </td></tr>
<tr><td>sementes    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Lista de todos os endereços IP de saudação que são designados como sementes.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Isso é usado por Olá NetworkTopologyStrateg inferindo Olá data center e rack de saudação do hello VM</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Etapa 6: Capturar a imagem da VM Olá
Faça logon na máquina virtual de saudação usando Olá hostname (hk-cas-template.cloudapp.net) e a chave privada de SSH de saudação criado anteriormente. Consulte como tooUse SSH com Linux no Azure para detalhes sobre como toolog usando Olá comando ssh ou putty.exe.

Execute Olá sequência da imagem de saudação toocapture ações a seguir:

##### <a name="1-deprovision"></a>1. Desprovisionar
Use o comando hello "sudo waagent – desprovisionamento + user" tooremove informações específicas da instância de máquina Virtual. Consulte para [como tooCapture uma máquina Virtual Linux](capture-image.md) tooUse como um modelo de obter mais detalhes sobre o processo de captura de imagem de saudação.

##### <a name="2-shutdown-hello-vm"></a>2: Olá desligar VM
Certifique-se de que a máquina virtual hello está realçada e clique Olá desligamento link na barra de comandos Olá inferior.

##### <a name="3-capture-hello-image"></a>3: captura de imagem de saudação
Certifique-se de que a máquina virtual hello está realçada e clique Olá captura link na barra de comandos Olá inferior. Na próxima tela de Olá, dê um nome de imagem (por exemplo, hk-cas-2-08-ub-14-04-2014071), apropriado a descrição da imagem e clique em processo de captura do hello "Verificar" marca toofinish hello.

Isso levará alguns segundos e imagem Olá deve estar disponível na seção de Minhas imagens da Galeria de imagens de saudação. VM de origem Hello será excluída automaticamente após a imagem de saudação é capturada com êxito. 

## <a name="single-region-deployment-process"></a>Processo de implantação de região única
**Etapa 1: Criar rede Virtual de saudação** login Olá portal do Azure e criar uma rede virtual (clássica) com atributos Olá Olá a tabela a seguir mostrada. Consulte [criar uma rede virtual (clássica) usando o portal do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obter etapas detalhadas do processo de saudação.      

<table>
<tr><th>Nome do atributo da VM</th><th>Valor</th><th>Comentários</th></tr>
<tr><td>Nome</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>Região</td><td>Oeste dos EUA</td><td></td></tr>
<tr><td>Servidores DNS</td><td>Nenhum</td><td>Ignore isso, pois não estamos usando um servidor DNS</td></tr>
<tr><td>Espaço de endereço</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>IP Inicial</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Adicione Olá seguintes sub-redes:

<table>
<tr><th>Nome</th><th>IP Inicial</th><th>CIDR</th><th>Comentários</th></tr>
<tr><td>web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Subrede do farm da web de saudação</td></tr>
<tr><td>data</td><td>10.1.2.0</td><td>/24 (251)</td><td>Sub-rede para nós de banco de dados de saudação</td></tr>
</table>

Subredes da Web e dados podem ser protegidos por meio de grupos de segurança de rede cobertura de saudação do qual está fora do escopo deste artigo.  

**Etapa 2: Provisionar máquinas de virtuais** usando a imagem de saudação criada anteriormente, criaremos Olá seguintes máquinas virtuais na nuvem Olá servidor "hk-c-svc-Oeste" e associá-las toohello respectivas sub-redes conforme mostrado abaixo:

<table>
<tr><th>Nome da máquina    </th><th>Sub-rede    </th><th>Endereço IP    </th><th>Conjunto de disponibilidade</th><th>DC/Rack</th><th>Propagar?</th></tr>
<tr><td>hk-c1-west-us    </td><td>data    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>Sim</td></tr>
<tr><td>hk-c2-west-us    </td><td>data    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>Não </td></tr>
<tr><td>hk-c3-west-us    </td><td>data    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Sim</td></tr>
<tr><td>hk-c4-west-us    </td><td>data    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Não </td></tr>
<tr><td>hk-c5-west-us    </td><td>data    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Sim</td></tr>
<tr><td>hk-c6-west-us    </td><td>data    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Não </td></tr>
<tr><td>hk-c7-west-us    </td><td>data    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Sim</td></tr>
<tr><td>hk-c8-west-us    </td><td>data    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Não </td></tr>
<tr><td>hk-w1-west-us    </td><td>web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
<tr><td>hk-w2-west-us    </td><td>web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
</table>

Criação de saudação acima da lista de VMs requer Olá processo a seguir:

1. Crie um serviço de nuvem vazio em uma determinada região
2. Criar uma VM da imagem capturada anteriormente hello e anexá-lo a rede virtual do toohello criado anteriormente; Repita essa etapa para todas as VMs Olá
3. Adicionar um serviço de nuvem de toohello de Balanceador de carga interno e anexá-lo a sub-rede toohello "dados"
4. Para cada VM criada anteriormente, adicione um ponto de extremidade com balanceamento de carga para tráfego de thrift por meio de um balanceador de carga interno com balanceamento de carga conjunto conectado toohello criada anteriormente

Olá acima processo pode ser executado usando o portal clássico do Azure; Use um computador Windows (use uma VM no Azure se você não tiver uma máquina com Windows tooa acesso), use Olá tooprovision de script do PowerShell a seguir todas as 8 VMs automaticamente.

**Lista 1: script do PowerShell para provisionamento de máquinas virtuais**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Etapa 3: configurar o Cassandra em cada VM**

Faça logon no hello VM e executar Olá seguinte:

* Edite $CASS_HOME/conf/cassandra-rackdc.properties toospecify Olá data center e rack propriedades:
  
       dc =EASTUS, rack =rack1
* Edite nós de propagação de tooconfigure cassandra.yaml como abaixo:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Etapa 4: Iniciar VMs hello e testar a saudação do cluster**

Log em um de nós de saudação (por exemplo, Hong Kong-c1-Oeste-us) e execução Olá seguindo o status do comando toosee saudação do cluster hello:

       nodetool –h 10.1.2.4 –p 7199 status

Você deve ver Olá exibição semelhante toohello um abaixo de um cluster de 8 nós:

<table>
<tr><th>Status</th><th>Endereço    </th><th>Carregar    </th><th>Tokens    </th><th>Possui </th><th>ID do host    </th><th>Rack</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38,0%    </td><td>Guid (removido)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>Guid (removido)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>Guid (removido)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Saudação de teste único Cluster de região
Use Olá cluster de saudação do tootest as etapas a seguir:

1. Usando Olá Powershell comando Get-AzureInternalLoadbalancer commandlet, obter o endereço IP de saudação do balanceador de carga interno de saudação (por exemplo  10.1.2.101). sintaxe de saudação do comando de saudação é mostrado abaixo: Get-AzureLoadbalancer – ServiceName "hk-c-svc-Oeste-us" [exibe detalhes de saudação do balanceador de carga interno Olá junto com seu endereço IP]
2. Faça logon no farm de web hello VM (por exemplo, Hong Kong-w1-Oeste-us) usando Putty ou ssh
3. Execute $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Use Olá CQL tooverify de comandos a seguir se Olá cluster está funcionando:
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');
   
     SELECT * FROM Customers;

Você deve ver uma exibição como Olá abaixo:

<table>
  <tr><th> customer_id </th><th> nome </th><th> Sobrenome </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

Observe que keyspace Olá criado na etapa 4 usa SimpleStrategy com um replication_factor de 3. SimpleStrategy é recomendado para implantações únicas de data center, enquanto NetworkTopologyStrategy é recomendado para implantações de vários data centers. Um replication_factor de 3 fornecerá tolerância às falhas do nó.

## <a id="tworegion"> </a>Processo de implantação de várias regiões
Será aproveitar a implantação de região única Olá concluída e repita Olá mesmo processo para instalar a segunda área de saudação. Olá principal diferença entre hello único e implantação de várias regiões é a configuração de túnel VPN Olá para comunicação entre região; Vamos começar com a instalação de rede hello, provisionar máquinas virtuais de saudação e configurar Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Etapa 1: Criar hello rede Virtual no hello 2º região
Faça logon no hello portal clássico do Azure e criar uma rede Virtual com hello Mostrar de atributos na tabela de saudação. Consulte [configurar uma rede Virtual somente em nuvem no portal clássico do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obter etapas detalhadas do processo de saudação.      

<table>
<tr><th>Nome do atributo    </th><th>Valor    </th><th>Comentários</th></tr>
<tr><td>Name    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>Região    </td><td>Leste dos EUA</td><td></td></tr>
<tr><td>Servidores DNS        </td><td></td><td>Ignore isso, pois não estamos usando um servidor DNS</td></tr>
<tr><td>Configurar uma VPN ponto a site</td><td></td><td>        Ignore isso</td></tr>
<tr><td>Configurar uma VPN site a site</td><td></td><td>        Ignore isso</td></tr>
<tr><td>Espaço de endereço    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>IP Inicial    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Adicione Olá seguintes sub-redes:

<table>
<tr><th>Nome    </th><th>IP Inicial    </th><th>CIDR    </th><th>Comentários</th></tr>
<tr><td>web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Subrede do farm da web de saudação</td></tr>
<tr><td>data    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Sub-rede para nós de banco de dados de saudação</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Etapa 2: criar Redes Locais
Uma rede Local na rede virtual do Azure é um espaço de endereço de proxy que mapeia o site remoto tooa, incluindo uma nuvem privada ou outra região do Azure. Este espaço de endereço de proxy é tooa associado o gateway remoto para roteamento toohello rede direito destinos de sistema de rede. Consulte [configurar uma Conexão de tooVNet de VNet](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) para obter instruções sobre como estabelecer a conexão de rede virtual a rede hello.

Crie duas redes locais por Olá detalhes a seguir:

| Nome da rede | Endereço do Gateway da VPN | Espaço de endereço | Comentários |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |Ao criar hello rede Local oferecem um espaço reservado para o endereço de gateway. endereço de gateway real Olá é preenchido quando Olá gateway é criado. Certifique-se de espaço de endereço Olá corresponde exatamente Olá respectiva rede virtual remota; Nesse caso hello rede virtual criado no hello região Leste dos EUA. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |Ao criar hello rede Local oferecem um espaço reservado para o endereço de gateway. endereço de gateway real Olá é preenchido quando Olá gateway é criado. Certifique-se de espaço de endereço Olá corresponde exatamente Olá respectiva rede virtual remota; Nesse caso hello rede virtual criado no hello região Oeste dos EUA. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Etapa 3: Mapa "Local" rede toohello VNETs do respectivos
De Olá portal clássico do Azure, selecione cada rede virtual, clique em "Configurar", verifique "Conectar toohello local rede" e selecione Olá de redes locais por Olá detalhes a seguir:

| Rede Virtual | Rede Local |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Etapa 4: criar Gateways em VNET1 e VNET2
No painel de saudação de ambas as redes virtuais hello, clique criar GATEWAY que irá disparar o processo de provisionamento do gateway VPN hello. Depois de alguns minutos Olá painel de cada rede virtual deve exibir o endereço de gateway real hello.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Etapa 5: Redes de "Local" atualização com endereços de Gateway do respectivos"" hello
Edite os dois Olá redes locais tooreplace Olá espaço reservado gateway IP endereço com endereço IP real de saudação do hello apenas provisionado gateways. Use Olá mapeamento a seguir:

<table>
<tr><th>Rede Local    </th><th>Gateway de Rede Virtual</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>Gateway de hk-vnet-west-us</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>Gateway de hk-vnet-east-us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Etapa 6: Atualizar a chave compartilhada Olá
Saudação de uso após a chave do Powershell script tooupdate Olá IPSec de cada gateway VPN [usar Olá mesma chave para ambos os gateways Olá]: hk-lnet-map-to-west-us LocalNetworkSiteName - conjunto-AzureVNetGatewayKey - VNetName hk-vnet-Leste-us - SharedKey D9E76BKK Conjunto AzureVNetGatewayKey - VNetName hk-vnet-Oeste-us - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Etapa 7: Estabeleça conexão Olá VNET para VNET
De Olá portal clássico do Azure, use o menu de "Painel" de saudação de ambas as conexão de gateway a gateway tooestablish Olá redes virtuais. Use itens de menu "Conectar-se" Olá, na barra de ferramentas do hello inferior. Depois de alguns minutos painel Olá deve exibir detalhes de conexão Olá graficamente.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Etapa 8: Criar máquinas virtuais de saudação na região #2
Criar imagem de Ubuntu Olá conforme descrito na implantação de região #1 pela seguinte Olá mesmo etapas ou copiar Olá imagem VHD arquivo toohello conta de armazenamento Azure localizada na região #2 e criar imagem hello. Usar essa imagem e criar hello seguindo a lista de máquinas virtuais em um novo serviço de nuvem hk-c-svc-Leste-nos:

| Nome da máquina | Sub-rede | Endereço IP | Conjunto de disponibilidade | DC/Rack | Propagar? |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |data |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Sim |
| hk-c2-east-us |data |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Não |
| hk-c3-east-us |data |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |Sim |
| hk-c5-east-us |data |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Sim |
| hk-c6-east-us |data |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Não |
| hk-c7-east-us |data |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Sim |
| hk-c8-east-us |data |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Não |
| hk-w1-east-us |web |10.2.1.4 |hk-w-aset-1 |N/D |N/D |
| hk-w2-east-us |web |10.2.1.5 |hk-w-aset-1 |N/D |N/D |

Siga Olá mesmo instruções como região #1 mas usam o espaço de endereço 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Etapa 9: configurar o Cassandra em cada VM
Faça logon no hello VM e executar Olá seguinte:

1. Editar $CASS_HOME/conf/cassandra-rackdc.properties toospecify Olá center e rack propriedades de dados em formato de saudação: dc = rack EASTUS = rack1
2. Editar nós de propagação de tooconfigure cassandra.yaml: sementes: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>Etapa 10: iniciar o Cassandra
Faça logon em cada VM e inicie Cassandra no plano de fundo Olá executando o comando a seguir de saudação: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Cluster de várias regiões de saudação de teste
Agora Cassandra foi implantado too16 nós com 8 nós em cada região do Azure. Esses nós estão em Olá mesmo cluster por meio de nome de cluster comum hello e a configuração de nó de semente hello. Use Olá cluster de saudação do processo tootest a seguir:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Etapa 1: Obter Olá IP de Balanceador de carga interno para ambas as regiões hello usando o PowerShell
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-west-us"
* Get-AzureInternalLoadbalancer -ServiceName "hk-c-svc-east-us"  
  
    Observe os endereços IP hello (por exemplo, oeste - 10.1.2.101 Leste - 10.2.2.101) exibido.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Etapa 2: Execute o seguinte de saudação na região oeste de saudação depois de fazer logon em Hong Kong-w1-Oeste-us
1. Execute $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Execute Olá comandos CQL a seguir:
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { 'class' : 'NetworkToplogyStrategy', 'WESTUS' : 3, 'EASTUS' : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Você deve ver uma exibição como Olá abaixo:

| customer_id | nome | Sobrenome |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Etapa 3: Execute o seguinte Olá na região Leste de saudação depois de fazer logon em Hong Kong-w1-Leste-nos:
1. Execute $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Execute Olá comandos CQL a seguir:
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, 'Jane', 'Doe');   SELECT * FROM Customers;

Você deve ver Olá mesmo exibir como visto para região oeste de saudação:

| customer_id | nome | Sobrenome |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

Executar inserções mais alguns e ver que os obtenham replicado toowest-us faz parte do cluster de saudação.

## <a name="test-cassandra-cluster-from-nodejs"></a>Testar o cluster de Cassandra do Node.js
Usando uma das VMs do Linux Olá criado anteriormente na camada de "web" Olá, podemos executará um simples Node. js script tooread Olá inserida anteriormente de dados

**Etapa 1: instalar o Node.js e o cliente do Cassandra**

1. Instale o Node.js e npm
2. Instale o pacote de nó "cassandra-client" usando npm
3. Execute Olá script no prompt de shell Olá que exibe a cadeia de caracteres de json de Olá Olá recuperada dados a seguir:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusão
Microsoft Azure é uma plataforma flexível que permite a execução de saudação da Microsoft, bem como software livre conforme demonstrado por este exercício. Clusters de Cassandra altamente disponíveis podem ser implantados em um único data center por meio de saudação distribuindo Olá nós de cluster em vários domínios de falha. Os clusters de Cassandra também podem ser implantados em regiões geograficamente distantes do Azure para sistemas à prova de desastres. Azure e habilita juntas Cassandra Olá construção de altamente escalonável, altamente disponível e os serviços de nuvem recuperáveis de desastres necessário pela internet de hoje dimensionar serviços.  

## <a name="references"></a>Referências
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

