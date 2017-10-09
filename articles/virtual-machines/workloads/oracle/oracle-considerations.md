---
title: "soluções de aaaOracle no Microsoft Azure | Microsoft Docs"
description: "Saiba mais sobre configurações com suporte e as limitações das soluções da Oracle no Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Soluções da Oracle e sua implantação no Microsoft Azure
Este artigo aborda informações toosuccesfully necessário implantar várias soluções de Oracle no Microsoft Azure. Essas soluções são baseadas em imagens de máquina Virtual publicadas pela Oracle em hello Azure Marketplace. tooget uma lista de imagens disponíveis no momento, execute Olá comando a seguir:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
A partir da lista de saudação 6-16-2017 de imagens são seguinte hello:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Essas imagens são consideradas "Traga sua própria licença" e como tal, você só será cobrado pelos custos de computação, armazenamento e rede incorridos na execução de uma VM.  Presume-se estão corretamente licenciados toouse Oracle software e se você tem um contrato de suporte no local com o Oracle. Oracle tem garantia de mobilidade de licença de tooAzure local. Consulte Olá publicado [Oracle e Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Observação para obter detalhes sobre mobilidade de licença. 

Indivíduos também podem escolher toobase suas soluções em imagens personalizadas, eles criar do zero no Azure ou carregar um imagens personalizadas de seus ambientes locais no.

## <a name="support-for-jd-edwards"></a>Suporte para JD Edwards
Observação de suporte tooOracle de acordo com [Doc ID 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , versões JD Edwards EnterpriseOne 9.2 e superior têm suporte em **ofertas de nuvem de qualquer pública** que atenda aos seu específico `Minimum Technical Requirements` (MTR).  Você precisará toocreate imagens personalizadas que atendem às suas especificações MTR para o sistema operacional e software de compatibilidade do aplicativo. 

## <a name="oracle-database-virtual-machine-images"></a>Imagens de máquina virtual no Oracle Database
A Oracle oferece suporte às edições Oracle DB 12.1 Standard e Enterprise em execução no Azure em imagens de máquina virtual com base no Oracle Linux.  Para obter melhor desempenho para cargas de trabalho de produção do banco de dados Oracle no Azure hello, ser se tooproperly tamanho Olá a imagem da VM e usar discos gerenciados que contam com armazenamento Premium. Para obter instruções sobre como tooquickly obter um banco de dados Oracle em execução no Azure usando Olá Oracle publicadas imagem VM, [tente Olá instruções passo a passo de início rápido do banco de dados Oracle](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Opções de configuração de disco anexado

Discos anexados contam Olá serviço de armazenamento de BLOBs do Azure. Cada disco padrão pode fornecer uma velocidade máxima teórica de aproximadamente 500 IOPS (operações de entrada/saída por segundo). Nossa oferta de disco premium é preferível para cargas de trabalho de banco de dados de alto desempenho e pode obter o too5000 IOps por disco. Embora você possa usar um único disco se que atende o desempenho precisa - você pode melhorar o desempenho de IOPS eficaz Olá se você usa vários discos anexados, distribuir os dados do banco de dados entre eles e, em seguida, usa o Oracle Automatic Storage Management (ASM). Veja [Visão geral do armazenamento automático da Oracle](http://www.oracle.com/technetwork/database/index-100339.html) para obter mais informações específicas do Oracle ASM. Para obter um exemplo de como tooinstall e configurar o Oracle ASM em uma VM do Azure Linux - você pode tentar Olá [instalando e configurando o Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.

### <a name="oracle-realtime-application-cluster-rac"></a>Cluster de aplicativo em tempo real da Oracle (RAC)
Oracle RAC é projetado toomitigate Olá falha de um único nó em uma configuração de vários nós de cluster local.  Ele se baseia em duas tecnologias de locais que não são ambientes de nuvem pública nativo toohyper escala: multicast rede e disco compartilhado. Há soluções de terceiros criadas por outras empresas [como FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) que emulam essas tecnologias se você precisar toodeploy Oracle RAC no Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Considerações sobre alta disponibilidade e recuperação de desastres
Ao usar bancos de dados Oracle no Azure, você é responsável por implementar um tooavoid de solução de recuperação desastres e disponibilidade alta qualquer tempo de inatividade. 

É possível obter alta disponibilidade e recuperação de desastre para o Oracle Database Enterprise Edition (sem RAC) no Azure usando o [Data Guard, Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) ou o [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), com dois bancos de dados em duas máquinas virtuais separadas. Ambas as máquinas virtuais devem ser em Olá mesmo [rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure acessarem uns aos outros sobre o endereço IP privado persistente para o hello.  Além disso, é recomendável colocar máquinas virtuais de saudação no hello disponibilidade mesmo conjunto tooallow tooplace do Azure em separado domínios de falha e domínios de atualização.  Você deve toohave redundância geográfica - você pode ter dois bancos de dados replicar entre duas regiões diferentes e conecte-se duas instâncias de saudação com um Gateway de VPN.

Temos um tutorial "[implementar Oracle Data Guard no Azure](configure-oracle-dataguard.md)" que orienta tootrial de procedimento de configuração básica do hello isso no Azure.  

Com o Oracle Data Guard, a alta disponibilidade pode ser obtida com um banco de dados primário em uma máquina virtual, um banco de dados secundário (em espera) em outra máquina virtual e replicação unidirecional entre eles. resultado de saudação é acesso de leitura toohello cópia de banco de dados de saudação. Com o Oracle GoldenGate, você pode configurar a replicação bidirecional entre dois bancos de dados de saudação. toolearn como tooset uma solução de alta disponibilidade para bancos de dados usando essas ferramentas, consulte [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) e [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentação no site da Oracle hello. Se você precisa de leitura-gravação acesso toohello cópia de banco de dados hello, você pode usar [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Temos um tutorial "[implementar Oracle GoldenGate no Azure](configure-oracle-golden-gate.md)" que orienta Olá básico seup procedimento tootrial isso no Azure.

Apesar de ter uma solução de alta disponibilidade e recuperação de desastres projetada no Azure, você desejará tooensure tiver uma estratégia de backup em vigor toorestore seu banco de dados.  Temos um tutorial [Backup e recuperar um banco de dados Oracle](oracle-backup-recovery.md) que orienta você por meio do procedimento de saudação básicas para estabelecer um backup consistente –.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Imagens de máquina virtual do Oracle WebLogic Server
* **Há suporte para clustering apenas na Enterprise Edition.** Você está licenciado toouse cluster do WebLogic somente quando usar Olá Enterprise Edition do WebLogic Server. Não use clustering com a Standard Edition do WebLogic Server.
* **O multicast de protocolo UDP não tem suporte.** O Azure dá suporte a unicast UDP, mas não a multicast ou difusão. WebLogic Server é capaz de toorely em recursos do unicast UDP do Azure. Para melhores resultados com base no unicast UDP, é recomendável que o tamanho de cluster do WebLogic Olá seja mantida estático, ou ser mantido com não mais de 10 servidores gerenciados incluídos no cluster hello.
* **WebLogic Server espera Olá toobe de portas públicas e privadas de acesso mesmo para T3 (por exemplo, ao usar o Enterprise JavaBeans).** Considere um cenário de várias camadas em que um aplicativo de serviço de camada (EJB) está em execução em um cluster do WebLogic Server que consiste em duas ou mais VMs, em uma vNet chamada **SLWLS**. camada de saudação do cliente está em uma sub-rede diferente no hello mesma rede virtual, execução de um programa Java simple tentar toocall EJB na camada de serviço hello. Como camada de serviço necessárias tooload saldo hello, um ponto de extremidade público com balanceamento de carga precisa toobe criado para Olá máquinas virtuais no cluster do WebLogic Server da saudação. Se a porta privada de saudação que você especificar for diferente da porta pública da saudação (por exemplo, 7006: 7008), ocorrerá um erro, como a seguir hello:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Isso ocorre porque para qualquer acesso T3 remoto, WebLogic Server espera que a porta do balanceador de carga hello e Olá gerenciado do WebLogic server porta toobe Olá mesmo. No hello acima caso, Olá cliente está acessando a porta 7006 (porta do balanceador de carga Olá) e servidor gerenciado hello está escutando a 7008 (porta privada de saudação). Essa restrição se aplica somente ao acesso T3, não HTTP.

   tooavoid esse problema, use uma das Olá soluções alternativas a seguir:

  * Use Olá mesmo privada e números de porta público de carga balanceada dedicados de pontos de extremidade tooT3 acesso.
  * Inclua Olá seguinte parâmetro JVM ao iniciar o WebLogic Server:

         -Dweblogic.rjvm.enableprotocolswitch=true

Para obter informações relacionadas, veja o artigo **860340.1** da Base de Conhecimentos em <http://support.oracle.com>.

* **Limitações de balanceamento de carga e clustering dinâmico.** Suponha que você deseja toouse um cluster dinâmico no WebLogic Server e expô-lo por meio de um único público com balanceamento de carga de ponto de extremidade no Azure. Isso pode ser feito desde que você usar um número de porta fixa para cada um dos hello (atribuídos dinamicamente de um intervalo) de servidores gerenciados e não iniciar mais servidores gerenciados que as máquinas para acompanhar administrador hello (ou seja, não mais de um servidor gerenciado por virt ual máquina). Se sua configuração resulta em mais servidores do WebLogic sendo iniciados do que há máquinas virtuais (ou seja, onde várias compartilhamento de instâncias do WebLogic Server hello mesma máquina virtual), em seguida, não é possível que mais de uma das instâncias do WebLogic Server servidores tooa de toobind recebe o número da porta – Olá outros usuários na máquina virtual falhará.

   Em Olá outro lado, se você configurar Olá administrador server tooautomatically atribuir números de porta exclusivos tooits gerenciados, servidores de balanceamento de carga não é possível porque o Azure não oferece suporte a mapeamento de uma única porta pública toomultiple privada portas como seria necessário para essa configuração.
* **Várias instâncias do Weblogic Server em uma máquina virtual.** Dependendo dos requisitos de implantação, você pode considerar a opção Olá da execução de várias instâncias do WebLogic Server em hello mesma máquina virtual, se a máquina virtual de saudação é grande o suficiente. Por exemplo, em uma máquina virtual de tamanho médio, que contém dois núcleos, você poderia escolher toorun duas instâncias do WebLogic Server. No entanto, observe que ainda é recomendável que você evite introduzir pontos únicos de falha em sua arquitetura, o que seria o caso de Olá se você usou apenas uma máquina virtual que está executando várias instâncias do WebLogic Server. Usar pelo menos duas máquinas virtuais poderia ser uma abordagem melhor, e cada uma dessas máquinas virtuais poderia então executar várias instâncias do WebLogic Server. Cada uma dessas instâncias do WebLogic Server ainda pode fazer parte de saudação mesmo cluster. Observe, no entanto, atualmente não é possível toouse balancear tooload do Azure pontos de extremidade expostos por essas implantações do WebLogic Server em Olá mesma máquina virtual, porque o balanceador de carga do Azure requer Olá toobe de servidores com balanceamento de carga distribuída entre máquinas virtuais exclusivas.

## <a name="oracle-jdk-virtual-machine-images"></a>Imagens de máquina virtual no JDK do Oracle
* **Atualizações mais recentes do JDK 6 e 7.** Embora recomendemos usando a versão compatível mais recente público da saudação do Java (atualmente Java 8), Azure também disponibiliza JDK 6 e 7 imagens. Isso serve para aplicativos herdados que ainda não pronto toobe atualizado tooJDK 8 sejam. Enquanto as atualizações tooprevious JDK imagens podem não estar disponível toohello público em geral, determinada Olá Microsoft parceria com a Oracle, Olá JDK 6 e 7 imagens fornecidas pelo Azure são pretendido toocontain uma atualização mais recente não públicos que normalmente é oferecida por Oracle tooonly um grupo seleto de Oracle do suporte para os clientes. Novas versões de imagens do JDK Olá serão disponibilizadas ao longo do tempo com as versões atualizadas do JDK 6 e 7.

   Olá JDK disponível neste JDK 6 e 7 imagens e máquinas virtuais de saudação e imagens derivadas deles, só podem ser usadas dentro do Azure.
* **JDK de 64 bits.** imagens de máquina virtual do Oracle WebLogic Server Hello e imagens de máquina virtual do Oracle JDK Olá fornecidas pelo Azure contêm versões de 64 bits de saudação do Windows Server e Olá JDK.

## <a name="next-steps"></a>Próximas etapas
Agora, você tem uma visão geral das soluções atuais da Oracle no Microsoft Azure. A próxima etapa é toogo e implantar seu primeiro banco de dados Oracle no Azure.
- Tente Olá [criar um banco de dados Oracle no Azure](oracle-database-quick-create.md) tooget tutorial de Introdução.
