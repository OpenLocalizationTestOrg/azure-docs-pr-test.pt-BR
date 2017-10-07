---
title: "recuperação de desastres e disponibilidade de aaaHigh do SAP HANA no Azure (instâncias grandes) | Microsoft Docs"
description: "Estabeleça a alta disponibilidade e planeje a recuperação de desastre do SAP HANA no Azure (instâncias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>Alta disponibilidade e recuperação de desastre do SAP HANA (instâncias grandes) no Azure 

A alta disponibilidade e a recuperação de desastre são aspectos importantes da execução crucial do SAP HANA em servidores do Azure (instâncias grandes). Toowork importante de sua com o SAP, o integrador de sistema, ou arquiteto de tooproperly da Microsoft e implementar Olá estratégia direito alta-disponibilidade/recuperação de desastres. Também é importante tooconsider objetivo de ponto de recuperação de saudação e objetivo de tempo de recuperação, que são específicos de tooyour ambiente.

## <a name="high-availability"></a>Alta disponibilidade

Microsoft oferece suporte a métodos de alta disponibilidade da SAP HANA "fora da caixa hello," que incluem:

- **Replicação de armazenamento:** Olá tooreplicate de capacidade do sistema de armazenamento local de tooanother todos os dados (em, ou separado, Olá mesmo Data Center). O SAP HANA funciona independentemente desse método.
- **Replicação de sistema do HANA:** Olá replicação de todos os dados no sistema do SAP HANA tooa separado SAP HANA. o objetivo de tempo de recuperação Olá é minimizado por meio da replicação de dados em intervalos regulares. SAP HANA dá suporte a modos de na memória, síncronos e assíncronos, síncronos (recomendado para o SAP HANA sistemas que estão dentro do hello mesmo datacenter ou menos de 100 KM distância). No design atual de saudação de carimbos de instância grande HANA, replicação de sistema do HANA pode ser usada apenas para a alta disponibilidade.
- **Failover automático de host:** um toouse de solução de recuperação de falhas locais como uma alternativa toosystem de replicação. Quando o nó de saudação mestre fica indisponível, um ou mais nós do SAP HANA em espera são configurados no modo de expansão e SAP HANA passam automaticamente tooanother nó.

Para obter mais informações sobre a alta disponibilidade do SAP HANA, consulte Olá SAP informações a seguir:

- [Whitepaper de Alta Disponibilidade do SAP HANA](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [Guia de administração do SAP HANA](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [Vídeo do SAP Academy sobre Replicação do Sistema SAP HANA](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP Note de Suporte nº 1999880 – perguntas frequentes sobre replicação do sistema SAP HANA](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP Note de Suporte SAP nº 2165547 – backup e restauração do SAP HANA no ambiente de replicação do sistema SAP HANA](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP Note de Suporte SAP nº 1984882 – uso da replicação do sistema SAP HANA para troca de hardware com tempo de inatividade mínimo/zero](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Recuperação de desastre

O SAP HANA no Azure (Instâncias Grandes) é oferecido em duas regiões do Azure em uma região geopolítica. Entre dois carimbos de instância grande Olá das duas regiões diferentes é uma conectividade de rede direta para replicar dados durante a recuperação de desastres. replicação de saudação de dados saudação é com base na infraestrutura de armazenamento. replicação de saudação não é feita por padrão. Ele é feito para as configurações de cliente de saudação que ordenados a recuperação de desastres hello. No projeto atual do hello, replicação de sistema do HANA não pode ser usada para recuperação de desastres.

No entanto, tootake vantagem Olá recuperação de desastres, você precisa toostart toodesign Olá rede conectividade toohello duas regiões diferentes do Azure. toodo, portanto, é necessário uma conexão de circuito de rota expressa do Azure do local em sua região do Azure principal e outra conexão de circuito de região de recuperação de desastres tooyour local. Essa medida abrange uma situação em que uma região do Azure completa, incluindo local do MSEE (Microsoft Enterprise Edge Router), tem um problema.

Como uma segunda medida, você pode se conectar a redes virtuais do Azure que se conectam tooSAP HANA no Azure (instâncias grandes) em uma saudação regiões tooboth os circuitos de rota expressa. Essa medida trata um caso em que apenas um dos locais de MSEE Olá que se conecta a sua localização no local com o Azure fica fora de serviço.

Olá figura a seguir mostra a configuração ideal Olá para recuperação de desastres:

![Configuração ideal para a recuperação de desastre](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Olá, caso ideal para uma configuração de recuperação de desastres de rede de saudação é toohave dois circuitos de rota expressa do local toohello duas regiões diferentes do Azure. Um circuito vai tooregion #1, executando uma instância de produção. circuito de rota expressa segundo Olá vai tooregion #2, executando algumas instâncias do HANA de não produção. (Isso é importante se uma região do Azure inteira, incluindo hello MSEE e carimbo de data / instância grande ficar fora da grade hello.)

Como uma segunda medida, Olá várias redes virtuais é conectada toohello vários circuitos do ExpressRoute que estão conectado tooSAP HANA no Azure (instâncias grandes). Você pode ignorar Olá onde uma MSEE está falhando, local ou você pode reduzir o objetivo de ponto de recuperação Olá para recuperação de desastres, como abordamos mais tarde.

requisitos de Avançar Olá para uma configuração de recuperação de desastre são:

- Você deve solicitar o SAP HANA em SKUs do Azure (instâncias grandes) de saudação mesmo tamanho de sua produção SKUs e implantá-las na região de recuperação de desastres hello. Essas instâncias podem ser usado toorun teste, área restrita ou QA HANA instâncias.
- Você deve solicitar um perfil de recuperação de desastres para cada um dos seus SAP HANA em SKUs do Azure (instâncias grandes) que você deseja toorecover no site de recuperação de desastres hello, se necessário. Esta ação leva toohello alocação de volumes de armazenamento, que são alvo de saudação de replicação de armazenamento Olá da sua região de produção em região de recuperação de desastres hello.

Depois de atender a saudação anterior requisitos, é a replicação de armazenamento Olá responsabilidade toostart. Na infraestrutura de armazenamento Olá usada para o SAP HANA no Azure (instâncias grandes), a base de saudação de replicação de armazenamento é instantâneos de armazenamento. replicação de recuperação de desastres do toostart Olá, é necessário tooperform:

- Um instantâneo do LUN de inicialização conforme descrito anteriormente.
- Um instantâneo dos volumes relacionados ao HANA conforme descrito anteriormente.

Depois de executar esses instantâneos, a réplica inicial de volumes de saudação é propagada em volumes de saudação que estão associados ao seu perfil de recuperação de desastres na região de recuperação de desastres de saudação.

Subsequentemente, o instantâneo mais recente de armazenamento Olá é usado a cada hora deltas de saudação tooreplicate que desenvolvem em volumes de armazenamento de saudação.

objetivo de ponto de recuperação de saudação que é obtido com essa configuração é de 60 minutos too90. tooachieve uma melhor recuperação objetivo de ponto de caso de recuperação de desastres Olá, cópia Olá HANA transação backups de log do HANA SAP no Azure (instâncias grandes) toohello outra região do Azure. tooachieve este objetivo de ponto de recuperação, Olá a seguir:

1. Fazer backup de transação do HANA Olá backup de log com a frequência possível muito/hana/log /.
2. Copie backups de log de transações hello quando elas estiverem concluído tooan Azure VM (máquina virtual), que está em uma rede virtual que tenha se conectado toohello SAP HANA no servidor do Azure (instâncias grandes).
3. Dessa VM, copie Olá backup tooa VM que está em uma rede virtual na região de recuperação de desastres hello.
4. Manter backups de log de transação de Olá Olá VM nessa região.

Em caso de desastre, depois que o perfil de recuperação de desastres de saudação tiver sido implantado em um servidor real, copiem backups de log de transações Olá Olá VM toohello HANA SAP no Azure (instâncias grandes) que é servidor primário do hello agora na região de recuperação de desastres Olá, e Restaure os backups. A recuperação é possível porque o estado de saudação do HANA em discos de recuperação de desastres Olá é que um instantâneo do HANA. Este é o ponto de deslocamento de saudação para restaurações adicionais de backups de log de transações.

## <a name="backup-and-restore"></a>Backup e restauração

Um banco de dados de toooperating aspectos mais importantes Olá é verificar se o banco de dados de saudação pode ser protegido de vários eventos catastróficos. Esses eventos podem ser causados por qualquer coisa de erros de usuário toosimple desastres naturais.

Backup de um banco de dados com toorestore de capacidade de saudação-tooany ponto no tempo (como antes que alguém excluído dados críticos), permite que o estado de tooa de restauração mais próximo possível maneira toohello antes da interrupção Olá ocorreu.

Dois tipos de backup devem ser executados para obter melhores resultados:

- Backups de banco de dados
- Backups do log de transações

Além disso toofull backups de banco de dados executados em um nível de aplicativo, você pode ser ainda mais completa ao realizar backups com instantâneos de armazenamento. A execução de backups de log também é importante para restaurar o banco de dados da saudação (tooempty Olá logs e transações confirmadas já).

O SAP HANA no Azure (grandes instâncias) oferece duas opções de backup e de restauração:

- DIY (Faça Você Mesmo). Depois de calcular tooensure espaço em disco suficiente, execute backups completos de banco de dados e de log usando os métodos de backup em disco (toothose discos). Ao longo do tempo, os backups de saudação são copiado tooan conta de armazenamento do Azure (depois de configurar um servidor de arquivos baseado no Azure com armazenamento praticamente ilimitada) ou usam um cofre de Backup do Azure ou o armazenamento do Azure frio. Outra opção é toouse uma ferramenta de proteção de dados de terceiros, como Commvault, backups de saudação toostore depois que eles são copiados tooa conta de armazenamento. Olá DIY opção de backup também pode ser necessário para dados que precisa toobe armazenado por períodos mais longos para fins de auditoria e conformidade.
- Use Olá backup e restaurar a funcionalidade que Olá infraestrutura subjacente do HANA SAP no Azure (instâncias grandes) fornece. Essa opção atende a necessidade de saudação de backups e faz backups manuais quase obsoleto (exceto onde os backups de dados são necessários para fins de conformidade). rest Olá endereços essa seção Olá backup e restaurar a funcionalidade que é oferecida com HANA (instâncias grandes).

> [!NOTE]
> tecnologia de instantâneo de saudação que é usada pela infraestrutura subjacente de saudação do HANA (instâncias grandes) tem uma dependência em instantâneos do SAP HANA. Instantâneos do SAP HANA não funcionam junto com os Contêineres de Banco de Dados Multilocatário do SAP HANA. Como resultado, esse método de backup não pode ser usado toodeploy SAP HANA multilocatário banco de dados de contêineres.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Usando instantâneos de armazenamento do SAP HANA no Azure (Instâncias Grandes)

infraestrutura de armazenamento de saudação subjacente HANA SAP no Azure (instâncias grandes) oferece suporte à noção de saudação de um instantâneo de volumes de armazenamento. Backup e restauração de um volume específico são suportados, com hello considerações a seguir:

- Em vez de backups de banco de dados, instantâneos de volume de armazenamento são executados com frequência.
- instantâneo de armazenamento Olá inicia um instantâneo do SAP HANA antes de executar o instantâneo de armazenamento hello. Esse instantâneo SAP HANA é o ponto de instalação de saudação para restaurações de log eventual após a recuperação do instantâneo de armazenamento de saudação.
- Ponto de saudação onde o instantâneo de armazenamento Olá é executado com êxito, Olá SAP HANA é excluído.
- Backups de log são usados frequentemente e armazenados no volume de backup de log hello ou no Azure.
- Se o banco de dados de saudação deve ser restaurado tooa determinado ponto no tempo, é feita uma solicitação tooMicrosoft suporte do Azure (interrupção de produção) ou SAP HANA no gerenciamento de serviços do Azure toorestore tooa determinados instantâneo de armazenamento (por exemplo, uma planejado restauração de um sistema de área restrita tooits estado original).
- instantâneo do SAP HANA Olá que está incluído no instantâneo de armazenamento Olá é um ponto de deslocamento para a aplicação de backups de log que foram executados e armazenados depois Olá armazenamento instantâneo foi tirado.
- Esses backups de log são feitos toorestore tooa backup de banco de dados de saudação determinado ponto no tempo.

Backup de saudação especificando\_nome cria um instantâneo de saudação volumes a seguir:

- hana/data
- Hana/log
- Hana/log\_backup (montado como backup no hana/log)
- hana/shared

### <a name="storage-snapshot-considerations"></a>Considerações sobre o instantâneo de armazenamento

>[!NOTE]
>Os instantâneos de armazenamento _não_ são fornecidos gratuitamente, já que espaço de armazenamento adicional deve ser alocado.

mecanismos de saudação específico de instantâneos de armazenamento para o SAP HANA no Azure (instâncias grandes) incluem:

- Um instantâneo de armazenamento específico (a saudação momento quando ele é usado) consome muito pouco armazenamento.
- Como alterações de conteúdo de dados e conteúdo Olá dados SAP HANA alteração dos arquivos no volume de armazenamento hello, instantâneo Olá precisa de conteúdo do bloco toostore Olá original.
- instantâneo de armazenamento Olá aumenta de tamanho. instantâneo de hello mais Olá existir, maior instantâneo de armazenamento Olá Olá torna-se.
- Olá mais as alterações feitas toohello volume do banco de dados SAP HANA em tempo de vida de saudação de um instantâneo de armazenamento, torna-se aos consumo de espaço maior Olá de saudação do instantâneo de armazenamento de saudação.

SAP HANA no Azure (instâncias grandes) vem com tamanhos de volume fixo para o volume de dados e de log do SAP HANA hello. Executar instantâneos desses volumes consome em seu espaço de volume, portanto, é sua instantâneos de armazenamento responsabilidade tooschedule (dentro de saudação SAP HANA no processo do Azure [grandes instâncias]).

Olá seções a seguir fornecem informações para executar esses instantâneos, incluindo recomendações gerais:

- Embora o hardware Olá pode sustentar 255 instantâneos por volume, é altamente recomendável que você fique bem abaixo desse limite.
- Antes de executar instantâneos de armazenamento, monitore e mantenha o controle do espaço livre.
- Número mais baixo de saudação de instantâneos de armazenamento com base no espaço livre. Talvez seja necessário um número de saudação toolower de instantâneos que você mantenha ou talvez seja necessário tooextend volumes de saudação. (Você pode solicitar armazenamento adicional em unidades de 1 TB).
- Durante as atividades como a movimentação de dados em SAP HANA com ferramentas de migração do sistema (com R3load ou restaurando bancos de dados do SAP HANA de backups), é altamente recomendável não executar quaisquer instantâneos de armazenamento. (Se estiver sendo feita uma migração de sistema em um novo sistema SAP HANA, instantâneos de armazenamento não precisaria toobe executada.)
- Durante a maior reorganizações de tabelas do SAP HANA, instantâneos de armazenamento devem ser evitados se possível.
- Os instantâneos de armazenamento são uma recursos de recuperação de desastres Olá tooengaging pré-requisitos do HANA SAP no Azure (instâncias grandes).

### <a name="setting-up-storage-snapshots"></a>Configurar instantâneos de armazenamento

1. Certifique-se de que Perl está instalado no sistema de operacional Linux Olá no servidor do hello HANA (instâncias grandes).
2. Modificar/etc/ssh/ssh\_linha de saudação do config tooadd _MACs hmac-sha1_.
3. Crie uma conta de usuário de backup do SAP HANA no nó de saudação mestre para cada instância do SAP HANA (se aplicável) estão em execução.
4. cliente do SAP HANA HDB Olá deve ser instalado em todos os servidores do SAP HANA (instâncias grandes).
5. Olá primeiro SAP HANA (instâncias grandes) servidor de cada região, uma chave pública deve ser criada Olá tooaccess subjacente a infraestrutura de armazenamento que controla a criação do instantâneo.
6. Copie o script de saudação do azure\_hana\_backup.pl do local de instalação /scripts toohello **hdbsql** de saudação instalação SAP HANA.
7. Saudação de cópia HANABackupDetails.txt arquivo /scripts toohello mesmo local como Olá script Perl.
8. Modificar Olá HANABackupDetails.txt arquivo conforme necessário para as especificações do cliente apropriado hello.

### <a name="step-1-install-sap-hana-hdbclient"></a>Etapa 1: Instalar o HDBClient do SAP HANA

Olá Linux instalado em SAP HANA no Azure (instâncias grandes) inclui pastas hello e scripts de instantâneos de armazenamento do SAP HANA tooexecute necessário para fins de backup e recuperação de desastres. No entanto, é sua responsabilidade tooinstall SAP HANA HDBclient enquanto você estiver instalando o SAP HANA. (Microsoft instala nem Olá HDBclient nem SAP HANA.)

### <a name="step-2-change-etcsshsshconfig"></a>Etapa 2: Alterar/etc/ssh/ssh\_config

Altere /etc/ssh/ssh\_config adicionando a linha _MACs hmac-sha1_ conforme mostrado aqui:
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Etapa 3: Criar uma chave pública

No hello primeiro SAP HANA no servidor do Azure (instâncias grandes) em cada região do Azure, crie uma infraestrutura de armazenamento de saudação de tooaccess toobe de chave pública usada para que você possa criar instantâneos. chave pública Olá garante que uma senha não é necessário toosign no armazenamento de toohello e que as credenciais de senha não são mantidas. No Linux no servidor do SAP HANA (instâncias grandes) hello, execute Olá chave pública do comando toogenerate Olá a seguir:
```
  ssh-keygen –t dsa –b 1024
```
Olá novo local é _/root/.ssh/id\_dsa.pub. Não insira uma senha real, caso contrário, será necessário tooenter Olá senha cada vez que entrar. Em vez disso, pressione **Enter** duas vezes tooremove Olá insira o requisito de senha para entrar.

Verificar toomake-se de que a chave pública Olá foi corrigido conforme o esperado, alterando too/root/.ssh/ pastas e, em seguida, executar Olá **ls** comando. Se a chave de saudação estiver presente, você pode copiá-lo executando o comando a seguir de saudação:

![Chave pública é copiada executando este comando](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

Neste ponto, entre em contato com o SAP HANA no gerenciamento de serviços do Azure e fornecer a chave de saudação. Olá, representante usa Olá tooregister de chave pública no hello infra-estrutura de armazenamento subjacente.

### <a name="step-4-create-an-sap-hana-user-account"></a>Etapa 4: Criar uma conta de usuário do SAP HANA

Crie uma conta de usuário do SAP HANA no Studio de SAP HANA para fins de backup. Essa conta deve ter Olá seguintes privilégios: _Backup Admin_ e _catálogo leitura_. Neste exemplo, o nome de usuário de saudação SCADMIN é criado.

![Criando um usuário no Studio HANA](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Etapa 5: Autorizar a conta de usuário do SAP HANA Olá

Autorize a conta de usuário do SAP HANA hello (toobe usado pelos scripts de saudação sem a necessidade de autorização sempre Olá script é executado). Olá comando SAP HANA `hdbuserstore` permite a criação de saudação de uma chave de usuário do SAP HANA, que é armazenada em um ou mais nós do SAP HANA. chave de usuário Olá também permite Olá usuário tooaccess SAP HANA sem ter que toomanage suas senhas no hello script processo que será abordado mais adiante.

>[!IMPORTANT]
>Execução hello seguinte comando como `_root_`. Caso contrário, o script hello não pode funcionar corretamente.

Digite hello `hdbuserstore` comando da seguinte maneira:

![Digite o comando de hdbuserstore Olá](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

Olá seguinte exemplo, em que usuário Olá é SCADMIN01 e Olá hostname é lhanad01, comando Olá é:
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Gerencie todos os scripts de servidor único para instâncias de escala horizontal do HANA. Neste exemplo, a chave de SAP HANA Olá SCADMIN01 deve ser alterado para cada host de forma que reflita host Olá chave toohello relacionados. Ou seja, Olá conta backup SAP HANA é corrigida com número de instância de saudação de saudação HANA DB, **lhanad**. chave Olá deve ter privilégios administrativos no host de saudação a que é atribuído e usuário de backup Olá para expansão deve ter instâncias do SAP HANA de tooall de direitos de acesso.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Etapa 6: Copiar itens de pasta de /scripts Olá

A seguir Olá copiar itens do hello/scripts pasta (incluído na imagem Olá gold da instalação Olá) toohello diretório de trabalho para **hdbsql**. Para instalações atuais do HANA, esse diretório é /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Copiar itens a seguir se eles estiverem executando a expansão de saudação ou OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
arquivo de HANABackupCustomerDetails.txt Olá é modificável da seguinte maneira para uma implantação de expansão. É arquivo de configuração e controle de saudação para script hello executado instantâneos de armazenamento de saudação. Você deve ter recebido Olá _nome do Backup de armazenamento_ e _endereço de IP de armazenamento_ do SAP HANA no gerenciamento de serviços do Azure quando suas instâncias foram implantadas. Você não pode modificar a sequência de hello, ordenação ou espaçamento de qualquer uma das variáveis de saudação ou script hello não funciona corretamente.

Para uma implantação de expansão, o arquivo de configuração de saudação pareceria com:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Para uma configuração de expansão, o arquivo de HANABackupCustomerDetailsBW.txt Olá pareceria com:
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Atualmente, apenas o nó 1 detalhes são usados no script de instantâneo de saudação real HANA armazenamento. É recomendável que você teste tooor de acesso de todos os nós do HANA para que, se o nó de backup mestre Olá mudar, você já garante que qualquer outro nó poderá assumir seu lugar modificando detalhes Olá no nó 1.

toocheck para configurações de saudação correto no arquivo de configuração de saudação ou instâncias HANA toohello conectividade correta, executadas um dos Olá scripts a seguir:
- Para uma configuração de expansão (independente na carga de trabalho do SAP):

 ```
testHANAConnection.pl
```
- Para configurações de escala horizontal:

 ```
testHANAConnectionBW.pl
```

Certifique-se de que essa instância HANA mestre Olá tenha acesso tooall necessário HANA servidores. Não há nenhum script de toohello parâmetros, mas você deve concluir Olá apropriado HANABackupCustomerDetails HANABackupCustomerDetailsBW File para Olá script toorun corretamente. Porque somente Olá shell comando códigos de erro são retornados, não é possível para Olá script tooerror Verifique cada instância. Mesmo assim, o script hello fornecem alguns comentários úteis para toodouble verificação.

script de saudação toorun:
```
 ./testHANAConnection.pl
```
 Se o script hello com êxito obtém o status de saudação da instância do HANA Olá, ele exibe uma mensagem que a conexão do HANA Olá foi bem-sucedida.

Além disso, há um segundo tipo de script, você pode usar toosign de capacidade do servidor do toocheck Olá mestre HANA instância no armazenamento toohello. Antes de executar o azure Olá\_hana\_backup (\_bw). pl script, você deve executar o script seguinte hello. Se um volume não contém nenhum instantâneo, é impossível toodetermine se o volume de saudação é simplesmente vazio ou há um ssh Olá de tooobtain falha detalhes do instantâneo. Por esse motivo, o script hello executa duas etapas:

- Ele verifica que console Olá armazenamento está acessível.
- Ele cria um instantâneo de teste ou fictício para cada volume por instância do HANA.

Por esse motivo, instância do HANA Olá é incluída como um argumento. Novamente, não é possível tooprovide verificação de erros de conexão de armazenamento hello, mas o script hello fornece dicas úteis se houver falha de execução de saudação.

Olá script é executado como:
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Ou é executado como:
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
script Hello também exibe uma mensagem que você é capaz de toosign adequadamente tooyour implantado armazenamento locatário, que é organizado em torno de números de unidade lógica de saudação (LUNs) que são usados por instâncias de servidor de saudação que você possui.

Antes de executar backups de instantâneo em armazenamento primeiro hello, execute Olá Avançar scripts toomake-se de que a configuração hello está correta.

Depois de executar esses scripts, você pode excluir instantâneos Olá executando:
```
./removeTestStorageSnapshot.pl <hana instance>
```
Ou
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Etapa 7: Executar instantâneos sob demanda

Execute instantâneos sob demanda (bem como agendar instantâneos regulares usando cron) conforme descrito aqui.

Para configurações de expansão, execute Olá script a seguir:
```
./azure_hana_backup.pl lhanad01 customer 20
```
Para configurações de expansão, execute Olá script a seguir:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
script de expansão de saudação faz algumas adicional toomake verificando se todos os servidores do HANA podem ser acessados e todas as instâncias do HANA status de retorno apropriado da instância de saudação antes de continuar com a criação de instantâneos do SAP HANA ou armazenamento.

Olá argumentos a seguir é necessária:

- Olá HANA instância que necessitam de backup.
- prefixo de instantâneo Olá para instantâneo de armazenamento hello.
- número de saudação de toobe instantâneos mantido por prefixo específico hello.

```
./azure_hana_backup.pl lhanad01 customer 20
```

execução de saudação do script hello cria o instantâneo de armazenamento de saudação essas três fases distintas:

- Execute um instantâneo do HANA.
- Execute um instantâneo do armazenamento.
- Remova o instantâneo do HANA hello.

Execute script hello chamando-o por Olá HDB pasta do executável que ele foi copiado para o. Ele faz backup de pelo menos Olá volumes a seguir, mas também faz backup de qualquer volume que tem o nome da instância SAP HANA explícita Olá no nome do volume hello.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
período de retenção de saudação é estritamente administrado com número de saudação de instantâneos enviado como um parâmetro quando você executar o script hello (por exemplo, 20, mostrada anteriormente). Portanto Olá tempo é uma função do período de saudação do número de execução e hello de instantâneos na chamada de saudação do script hello. Se número Olá de instantâneos que são mantidos exceder o número de saudação que são nomeados como um parâmetro na chamada de saudação do script hello, Olá instantâneo mais antigo de armazenamento deste rótulo (no nosso caso anterior, _personalizado_) será excluído antes de é um novo instantâneo executado. Isso significa que número Olá que dar como último parâmetro da chamada Olá Olá é número Olá que você pode usar toocontrol Olá número de instantâneos.

>[!NOTE]
>Assim que você alterar o rótulo de hello, contando Olá começa novamente.

Você precisará tooinclude Olá HANA nome de instância que é fornecido pelo SAP HANA no gerenciamento de serviços do Azure como um argumento se eles estão criando instantâneos em ambientes de vários nós. Em ambientes de nó único, nome Olá Olá SAP HANA na unidade do Azure (instâncias grandes) é suficiente, mas o nome da instância do HANA Olá ainda é recomendável.

Além disso, você pode fazer backup volumes\LUNs de inicialização usando Olá mesmo script. Você deve fazer backup do volume de inicialização pelo menos uma vez ao executar o HANA pela primeira vez, embora seja recomendável o agendamento de backup semanal ou todas as noite para inicialização em cron. Em vez de adicionar um nome de instância do SAP HANA, inserir _inicialização_ como Olá argumento para o script hello da seguinte maneira:
```
./azure_hana_backup boot customer 20
```
Olá mesma política de retenção é permitida toohello também volume de inicialização. Use instantâneos sob demanda, conforme descrito anteriormente, para casos especiais, como durante uma atualização de pacote (EHP) de aprimoramento do SAP, ou quando você precisar toocreate um instantâneo de armazenamento distintos.

Nós o incentivamos instantâneos de armazenamento tooperform agendada usando cron e é recomendável que você use o mesmo script de saudação para todos os backups e necessidades de recuperação de desastres (modificação Olá script entradas toomatch Olá vários solicitado tempos de backup). Esses são todos agendadas de forma diferente no cron dependendo de seu tempo de execução: por hora, 12 horas, diária ou semanal. agendamento de cron Olá é projetado toocreate instantâneos de armazenamento que correspondem a saudação abordada anteriormente rótulos de retenção de backup externo de longo prazo. script Hello inclui comandos tooback backup de todos os volumes de produção, dependendo de sua frequência solicitada (dados e arquivos de log são feitos por hora, enquanto o volume de inicialização de saudação é feito backup diário).

as entradas Olá Olá cron script a seguir executadas a cada hora em Olá décimo minuto, cada 12 horas no hello décimo minuto e diariamente no hello décimo minuto. Olá cron trabalhos são criados de forma que apenas um instantâneo de armazenamento do SAP HANA ocorre durante a qualquer hora específica, que hello backups por hora e diários ocorra no hello (12:10 AM) a mesma hora. toohelp otimizar a criação do instantâneo e replicação, SAP HANA no gerenciamento de serviços do Azure fornece Olá recomendado tempo para você toorun seus backups.

saudação padrão cron /etc/crontab de agendamento é o seguinte:
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
Nas instruções de cron anterior hello, volumes do HANA hello (sem o volume de inicialização) obtém instantâneo com rótulo Olá por hora. Esses instantâneos, 66 são mantidos. Além disso, 14 instantâneos com rótulo de 12 horas Olá são mantidos. Você possivelmente obterá instantâneos a cada hora por três dias, além de instantâneos de 12 horas por outro quatro dias, o que lhe dá uma semana inteira de instantâneos.

Agendar dentro de cron pode ser difícil, porque somente um script deve ser executado em um determinado momento, a menos que os scripts de saudação são alternados por vários minutos. Se você quiser backups diários para retenção de longo prazo, um instantâneo diário é mantido junto com um instantâneo de 12 horas (com uma contagem de retenção de sete cada) ou instantâneo por hora Olá é escalonada tootake local 10 minutos mais tarde. Apenas um instantâneo diário é mantido no volume de produção de hello.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
frequências Olá listadas aqui são apenas exemplos. tooderive o número ideal de instantâneos, use Olá critérios a seguir:

- Requisitos de objetivo de tempo de recuperação para recuperação pontual.
- Uso de espaço.
- Requisitos do objetivo de ponto de recuperação e objetivo de tempo de recuperação de desastre em potencial.
- Execução eventual de backups completos de banco de dados do HANA em discos. Sempre que um backup completo do banco de dados em discos, ou _backint_ interface, que é executada, falha na execução de saudação de instantâneos de armazenamento. Se você planejar backups de banco de dados completo tooexecute sobre instantâneos de armazenamento, certifique-se de que a execução de saudação de instantâneos de armazenamento está desabilitada durante esse tempo.

>[!IMPORTANT]
> uso de Olá de instantâneos de armazenamento para backups do SAP HANA é válido somente quando os instantâneos de saudação são executados em conjunto com backups de log do SAP HANA. Esses log backups necessidade toobe toocover capaz de saudação períodos de tempo entre os instantâneos de armazenamento hello. Se você tiver definido um toousers de comprometimento de uma recuperação point-in-time de 30 dias, você precisa seguir hello:

- Capacidade tooaccess um instantâneo de armazenamento que é de 30 dias.
- Backups de log de contígua sobre Olá últimos 30 dias.

No intervalo de saudação de backups de log, crie um instantâneo do volume de backup de log Olá também. No entanto, ser tooperform-se de que os backups de log regular para que você possa:

- Backups de log de contígua de saudação necessário tooperform recuperações de point-in-time.
- Impedir que o volume de log do SAP HANA Olá falta de espaço.

Uma das últimas etapas de saudação é tooschedule logs de backup SAP HANA no SAP HANA Studio. destino de backup de log SAP HANA Olá é Olá criada especialmente hana/log\_volume backups com ponto de montagem de saudação do /hana/log/backups.

![Agendar logs de backup SAP HANA no Studio de SAP HANA](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

Você pode escolher os backups com frequência maior que 15 minutos. Alguns usuários até mesmo executam backups de log a cada minuto, entretanto não é recomendado _ficar acima_ de 15 minutos.

Olá última etapa é toocreate de backup (após a instalação inicial de saudação do SAP HANA) tooperform um arquivo com base em uma única entrada de backup que deve existir no catálogo de backup hello. Caso contrário, SAP HANA não pode iniciar os backups de log indicados.

![Faça um backup toocreate baseada em arquivo uma única entrada de backup](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Número de Olá monitoramento e o tamanho de instantâneos no volume de disco Olá

Em um volume de armazenamento específico, você pode monitorar o número de saudação de instantâneos e o consumo de armazenamento de saudação de instantâneos. Olá `ls` comando não mostra o diretório de instantâneos de saudação ou arquivos. No entanto, Olá comando do sistema operacional Linux `du` faz, com hello comandos a seguir:

- `du –sh .snapshot`apresenta o total de todos os instantâneos no diretório de instantâneos de saudação.
- `du –sh --max-depth=1`lista todos os instantâneos são salvos na pasta de .snapshot hello e tamanho de saudação de cada instantâneo.
- `du –hc`fornece o tamanho total de saudação usado por todos os instantâneos.

Use esses toomake comandos-se de que instantâneos de saudação que são executados e armazenados não estão consumindo todo o armazenamento de saudação em volumes de saudação.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Reduzindo o número de saudação de instantâneos em um servidor

Conforme explicado anteriormente, você pode reduzir o número de saudação de determinados rótulos de instantâneos que você armazena. Olá últimos dois parâmetros de saudação comando tooinitiate um instantâneo são um rótulo e hello o número de instantâneos que você deseja tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
No exemplo anterior de saudação, rótulo de instantâneo de saudação é _cliente_ e número de saudação de instantâneos com este toobe rótulo retidos _20_. Como responder o consumo de espaço toodisk, talvez você queira tooreduce número de saudação de instantâneos armazenados. número de saudação do tooreduce de instantâneos é toorun script Olá Olá último parâmetro conjunto too5 de modo fácil de saudação:
```
./azure_hana_backup.pl lhanad01 customer 5
```
Como resultado do script hello em execução com essa configuração, o número de saudação de instantâneos, incluindo Olá armazenamento novo instantâneo, é _5_.

 >[!NOTE]
 > Esse script reduz o número de saudação de instantâneos somente se o instantâneo anterior mais recente de saudação é de mais de uma hora antigo. script Hello não exclui os instantâneos que são menos de uma hora antigos.

Essas restrições são a funcionalidade de recuperação de desastres opcional toohello relacionados oferecida.

Se você não quiser mais toomaintain um conjunto de instantâneos com o prefixo, você pode executar o script hello com _0_ hello retenção número tooremove todos os instantâneos de correspondência de prefixo. No entanto, remover todos os instantâneos pode afetar recursos Olá de recuperação de desastres.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Recuperando o instantâneo mais recente de HANA toohello

No evento de saudação a experiência de um cenário de produção para baixo, o processo de saudação de recuperação de um instantâneo de armazenamento pode ser iniciado como um incidente do cliente com o SAP HANA no gerenciamento de serviços do Azure. Um cenário como esse inesperado poderá ser uma questão de alta urgência se dados foram excluídos de produção sistema Olá única forma e dados de saudação tooretrieve são o banco de dados de produção de hello toorestore.

Em hello outro lado, uma recuperação point-in-time pode ser baixa urgência e planejadas para dias de antecedência. Você pode planejar essa recuperação com o SAP HANA no Gerenciamento de Serviços do Azure em vez de gerar um problema de alta prioridade. Por exemplo, talvez planejamento tootry uma atualização de software SAP de saudação aplicando um novo pacote de aprimoramento e, em seguida, precisa toorevert fazer instantâneo tooa que representa o estado de saudação antes da atualização Olá EHP.

Antes de você emitir a solicitação Olá, é necessário toodo alguma preparação. SAP HANA na equipe de gerenciamento de serviços do Azure pode lidar com a solicitação de saudação e fornecer volumes Olá restaurado. Depois disso, é tooyou toorestore Olá HANA banco de dados com base em instantâneos de saudação. Aqui está como tooprepare para Olá solicitar:

>[!NOTE]
>A interface do usuário pode variar do hello capturas de tela, dependendo da saudação versão SAP HANA você estiver usando a seguir.

1. Decida qual toorestore de instantâneo. Somente o volume de hana/dados Olá seria restaurado, a menos que você está indicado o contrário.

2. Desligar a instância do HANA hello.

 ![Desligar a instância do HANA Olá](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Desmonte volumes de dados de saudação em cada nó de banco de dados do HANA. restauração de saudação do instantâneo Olá falhará se os volumes de dados de saudação não são desmontados.

 ![Desmontar volumes de dados de saudação em cada nó de banco de dados do HANA](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Abra uma restauração de saudação do suporte do Azure solicitação tooinstruct de um instantâneo específico.

 - Durante a restauração da saudação: SAP HANA no gerenciamento de serviços do Azure pode solicitar que você tooattend tooensure uma chamada de conferência que nenhum dado é se perder.

 - Após a restauração de saudação: SAP HANA no gerenciamento de serviços do Azure notifica quando Olá armazenamento instantâneo foi restaurado.

5. Após a conclusão do processo de restauração hello, remonte todos os volumes de dados.

 ![Montar novamente todos os volumes de dados](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Selecione as opções de recuperação do SAP HANA Studio, se eles não aparecer automaticamente quando você se reconectar tooHANA banco de dados por meio do SAP HANA Studio. Olá, exemplo a seguir mostra um restauração toohello último HANA instantâneo. Um instantâneo de armazenamento incorpora um instantâneo do HANA e se você estiver restaurando o instantâneo mais recente de armazenamento toohello, ele deve ser instantâneo mais recente de HANA hello. (Se você estiver restaurando tooolder instantâneos de armazenamento, você precisa toolocate Olá HANA instantâneo com base em Olá tempo Olá armazenamento instantâneo foi tirado.)

 ![Selecionar as opções de recuperação no SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Selecione **recuperar Olá banco de dados tooa específico de backup ou armazenamento de instantâneo de dados**.

 ![janela de "Especificar o tipo de recuperação" Hello](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Selecione **Especificar backup sem catálogo**.

 ![janela de "Especificar o local de Backup" Hello](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. Em Olá **tipo de destino** lista, selecione **instantâneo**.

 ![janela de "Especificar Olá Backup tooRecover" Hello](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Clique em **concluir** toostart processo de recuperação de saudação.

 ![Clique em "Concluir" processo de recuperação de saudação toostart](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. o banco de dados do Hello HANA é restaurado e recuperado instantâneo do HANA toohello que está incluído no instantâneo de armazenamento hello.

 ![Banco de dados do HANA é restaurado e recuperado toohello instantâneo do HANA](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Recuperando o estado mais recente do toohello

Olá processo a seguir restaura o instantâneo do HANA Olá que está incluído no instantâneo de armazenamento hello. Ele restaura em seguida Olá transaction log backups toohello estado mais recente do banco de dados de saudação antes de restaurar o instantâneo de armazenamento hello.

>[!IMPORTANT]
>Antes de continuar, verifique se você tem uma cadeia completa e contígua de backups de log de transações. Sem esses backups, é possível restaurar o estado atual de saudação do banco de dados de saudação.

1. Conclua as etapas 1 a 6 de saudação que precedem o procedimento em "Recuperação toohello instantâneo mais recente HANA."

2. Selecione **recuperar o estado mais recente do hello banco de dados tooits**.

 ![Selecione "Recuperar o estado mais recente do tooits Olá banco de dados"](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Especifique o local de Olá Olá mais recentes HANA de backups de log. local de saudação precisa toocontain todos os backups de log de transações do HANA do estado mais recente do toohello Olá HANA instantâneo.

 ![Especificar local de Olá Olá mais recentes HANA de backups de log](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Selecione um backup como uma base de banco de dados que toorecover hello. Em nosso exemplo, isso é instantâneo do HANA Olá que foi incluído no instantâneo de armazenamento hello. (Apenas um instantâneo está listado no hello captura de tela a seguir).

 ![Selecione um backup como uma base de banco de dados que toorecover Olá](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Olá limpar **usar Backups de Delta** caixa de seleção se não existirem deltas entre o tempo de saudação do instantâneo do HANA hello e estado mais recente hello.

 ![Olá desmarque caixa de seleção "Usar Backups de Delta" se nenhum deltas existe](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Na tela de resumo hello, clique em **concluir** toostart procedimento de restauração de saudação.

 ![Clique em "Concluir" na tela de resumo da saudação](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Recuperando tooanother pontual
toorecover tooa ponto no tempo entre o instantâneo do HANA hello (incluído no instantâneo de armazenamento Olá) e outro que é posterior de saudação HANA instantâneo recuperação point-in-time, Olá a seguir:

1. Certifique-se de que você tenha todos os backups de log de transação do hello HANA instantâneo toohello tempo toorecover.
2. Iniciar Olá procedimento em "Recuperação toohello mais recente estado".
3. Na etapa 2 do procedimento hello, Olá **especificar tipo de recuperação** janela, selecione **a seguir recuperar Olá banco de dados toohello ponto no tempo**, especifique Olá ponto no tempo e, em seguida, conclua as etapas 3 a 6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Monitorando a execução de saudação de instantâneos

Você precisa de execução de saudação toomonitor de instantâneos de armazenamento. grava o arquivo de saída de tooa script Hello que executa um instantâneo de armazenamento e a salva toohello mesmo local que scripts Perl de saudação. Um arquivo separado é criado para cada instantâneo. saída de saudação de cada arquivo mostra claramente saudação várias fases que executa o script de instantâneo hello:

- Localizando um instantâneo de volumes Olá que precisam toocreate
- Localizando instantâneos Olá obtidos esses volumes
- Excluindo eventual existente instantâneos toomatch Olá número de instantâneos especificado
- Criando um instantâneo do HANA
- A criação de instantâneo de armazenamento Olá em volumes Olá
- Excluindo Olá HANA instantâneo
- Renomeando hello mais recente instantâneo muito**.0**

a parte mais importante saudação do script hello é a seguinte:
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
Você pode ver a este exemplo como registros de script Olá Olá criação do instantâneo do HANA hello. No caso de expansão Olá, esse processo é iniciado no nó mestre hello. nó mestre Olá inicia a criação de síncrona de saudação de instantâneos de saudação em cada um de nós de trabalho hello. Em seguida, Olá armazenamento instantâneo é obtido. Após a execução bem-sucedida do hello de instantâneos de armazenamento Olá, Olá HANA é excluído.
