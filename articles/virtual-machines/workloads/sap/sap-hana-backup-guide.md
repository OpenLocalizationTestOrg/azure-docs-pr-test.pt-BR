---
title: "Guia de aaaBackup do SAP HANA em máquinas virtuais do Azure | Microsoft Docs"
description: "O guia de backup do SAP HANA oferece duas possibilidades principais de backup para SAP HANA em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Guia de backup para SAP HANA em Máquinas Virtuais do Azure

## <a name="getting-started"></a>Introdução

Guia de backup de saudação do HANA SAP em execução em máquinas virtuais do Azure só descrevem os tópicos específicos do Azure. Para geral SAP HANA backup itens relacionados, verifique a documentação do SAP HANA hello (consulte _documentação de backup do SAP HANA_ posteriormente neste artigo).

Olá foco deste artigo é duas principais backup possibilidades para SAP HANA em máquinas virtuais do Azure:

- Sistema de arquivos de backup toohello HANA em uma máquina Virtual do Azure Linux (consulte [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md))
- Backup do HANA com base em instantâneos de armazenamento usando o recurso de instantâneo de blob de armazenamento do Azure Olá manualmente ou o serviço de Backup do Azure (consulte [backup SAP HANA com base em instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md))

SAP HANA oferece um backup de API, que permite que as ferramentas de backup de terceiros toointegrate diretamente com o SAP HANA. (Que não está dentro do escopo deste guia hello.) Não há nenhuma integração direta do SAP HANA com o Serviço de Backup do Azure disponível nessa API no momento.

SAP HANA oficialmente tem suporte no tipo de VM do Azure GS5 como instância única com cargas de trabalho de tooOLAP uma restrição adicional (consulte [localizar certificados de plataformas de IaaS](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) no site SAP Olá). Este artigo será atualizado conforme novas ofertas do SAP HANA forem disponibilizados para o Azure.

Há também uma solução híbrida do SAP HANA disponível no Azure, onde o SAP HANA é executado de forma não virtualizada em servidores físicos. No entanto, este guia de backup do Azure do SAP HANA abrange um ambiente puro do Azure onde o SAP HANA é executado em uma VM do Azure, sem ter o SAP HANA em execução em &quot;instâncias grandes.&quot; Consulte [Visão geral e arquitetura do SAP HANA (instâncias grandes) no Azure](hana-overview-architecture.md) para obter mais informações sobre essa solução de backup em &quot;instâncias grandes&quot; com base em instantâneos de armazenamento.

Informações gerais sobre produtos SAP com suporte no Azure podem ser encontradas em [SAP Observação 1928533](https://launchpad.support.sap.com/#/notes/1928533).

Olá três figuras a seguir oferecem uma visão geral da saudação opções de backup do SAP HANA usando recursos nativos do Azure no momento e também mostram três cenários possíveis de backup futuros. artigos relacionados do Hello [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md) e [backup SAP HANA com base em instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descrevem essas opções mais detalhadamente, incluindo considerações de tamanho e desempenho para SAP HANA backup de vários terabytes de tamanho.

![Esta figura mostra duas possibilidades para salvar o estado da VM atual Olá](media/sap-hana-backup-guide/image001.png)

Esta figura mostra a possibilidade de saudação de salvar Olá atual estado da VM, através de serviço de Backup do Azure ou instantâneo manual de discos de VM. Com essa abordagem, um &#39; não tem backups do SAP HANA toomanage. desafio de saudação do cenário de instantâneo do disco Olá é consistência do sistema de arquivos e um estado consistente com o aplicativo de disco. tópico de consistência de saudação é discutido na seção de saudação _consistência de dados SAP HANA ao armazenamento de instantâneos_ posteriormente neste artigo. Recursos e restrições do serviço de Backup do Azure relacionados a backups do HANA tooSAP também são discutidos neste artigo.

![Esta figura mostra opções para colocar um SAP HANA arquivo de backup dentro de saudação VM](media/sap-hana-backup-guide/image002.png)

Esta figura mostra opções para fazer um backup de arquivo do SAP HANA dentro Olá VM e, em seguida, armazenando-os arquivos de backup HANA em algum lugar outro uso de ferramentas diferentes. Fazer um backup do HANA requer mais tempo do que uma solução de backup do instantâneo, mas ele tem vantagens em relação à integridade e consistência. Mais detalhes são fornecidos neste artigo.

![Esta figura mostra um potencial futuro cenário de backup do SAP HANA](media/sap-hana-backup-guide/image003.png)

Esta figura mostra um potencial futuro cenário de backup do SAP HANA. Se o SAP HANA permitisse fazer backups a partir de uma replicação secundária, ele poderia adicionar mais opções para estratégias de backup. No momento não é possível postar tooa Olá SAP HANA Wiki de acordo com:

_&quot;É possível tootake backups no lado secundário Olá?_

_Não, atualmente pode apenas obter os dados e backups do lado primário da saudação de log. Se o backup de log automática estiver habilitada, após toohello tomada de lado secundário, os backups de log Olá automaticamente serão gravados existe.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Recursos do SAP para backup HANA

### <a name="sap-hana-backup-documentation"></a>Documentação de backup do SAP HANA

- [Introdução tooSAP HANA administração](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planejando sua estratégia de backup e recuperação](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [Agendar Backup HANA usando ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Agendar Backups de Dados (Ferramenta Cockpit do SAP HANA)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- Perguntas frequentes sobre o backup do SAP HANA em [Observação 1642148 do SAP](https://launchpad.support.sap.com/#/notes/1642148)
- Perguntas frequentes sobre instantâneos de banco de dados e armazenamento do SAP HANA em [Observação 2039883 do SAP](https://launchpad.support.sap.com/#/notes/2039883)
- Sistemas de arquivos de rede inadequados para backup e recuperação em [Observação 1820529 do SAP](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Por que o backup do SAP HANA?

Armazenamento do Azure oferece disponibilidade e confiabilidade imediato saudação (consulte [tooMicrosoft Introdução armazenamento do Azure](../../../storage/common/storage-introduction.md) para obter mais informações sobre o armazenamento do Azure).

Olá mínimo para &quot;backup&quot; é toorely em Olá SLAs do Azure, Olá manter arquivos de log e dados do SAP HANA no servidor de SAP HANA toohello anexado de VHDs do Azure VM. Essa abordagem abrange falhas VM, mas não possíveis danos toohello SAP HANA dados e arquivos de log ou erros lógicos, como a exclusão de arquivos de dados ou por engano. Os backups também são necessários por motivos legais ou de conformidade. Em resumo, sempre há a necessidade de backups do SAP HANA.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Como tooverify exatidão do backup do SAP HANA
Ao usar instantâneos de armazenamento, recomenda-se executar uma restauração de teste em um sistema diferente. Essa abordagem oferece um tooensure de forma que um backup está corretos e internos processos para o trabalho de backup e restauração conforme o esperado. Embora esse seja um problema significativo obstáculo no local, é muito mais fácil tooaccomplish na nuvem hello, fornecendo os recursos necessários temporariamente para essa finalidade.

Tenha em mente que fazer uma restauração simples e verificar se o HANA está ativo e em execução não são o suficiente. Idealmente, um deve ser executado um toobe de verificação de consistência de tabela se que esse banco de dados restaurado de saudação é bom. O SAP HANA oferece vários tipos de verificações de consistência descritos [Observação 1977584 do SAP](https://launchpad.support.sap.com/#/notes/1977584).

Informações sobre a verificação de consistência de tabela Olá também podem ser encontradas no site do SAP Olá em [tabela e verificações de consistência do catálogo](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Para backups de arquivos padrões, um teste de restauração não é necessário. Há duas ferramentas SAP HANA que ajudam a toocheck backups que podem ser usados para restauração: hdbbackupdiag e hdbbackupcheck. Consulte [Verificar manualmente se uma recuperação é possível](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) para obter mais informações sobre essas ferramentas.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Prós e contras do backup do HANA versus instantâneo do armazenamento

SAP & #39 t dê preferência tooeither HANA backup; em vez de instantâneo de armazenamento. Ela lista seus prós e contras, para que um possa determinar qual toouse dependendo da situação hello e tecnologia de armazenamento disponível (consulte [planejar sua estratégia de Backup e recuperação](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

No Azure, esteja atento ao fato de Olá Olá não de recurso de instantâneo de blob do Azure &#39; t para garantir a consistência do sistema de arquivo (consulte [usando instantâneos de blob com o PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Olá a próxima seção, _consistência de dados SAP HANA ao armazenamento de instantâneos_, aborda algumas considerações sobre esse recurso.

Além disso, uma tem toounderstand Olá implicações de cobranças ao trabalhar com instantâneos de blob frequentemente conforme descrito neste artigo: [Noções básicas sobre como os instantâneos acumulam cobranças](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— ela nem &#39; t tão óbvia como usar o Azure discos virtuais.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Consistência de dados do SAP HANA ao realizar instantâneos de armazenamento

A consistência de aplicativos e do sistema de arquivos é um problema complexo quando ao realizar instantâneos de armazenamento. problemas de tooavoid de maneira mais fácil Olá ser tooshut para baixo do SAP HANA ou talvez até mesmo a máquina virtual inteira de saudação. Um desligamento pode ser viável com uma demonstração ou protótipo ou até mesmo como um sistema de desenvolvimento, mas não é uma opção para um sistema de produção.

No Azure, um tem tookeep em mente que Olá não de recurso de instantâneo de blob do Azure &#39; t para garantir a consistência do sistema de arquivos. Ele funciona bem no entanto, usando Olá SAP HANA instantâneo recurso, como apenas um único disco virtual está envolvido. Mas mesmo com um único disco, itens adicionais toobe marcada. A [Observação 2039883 do SAP](https://launchpad.support.sap.com/#/notes/2039883) possui informações importantes sobre backups do SAP HANA por meio de instantâneos de armazenamento. Por exemplo, menciona que, com o sistema de arquivos XFS Olá, é necessário toorun **xfs\_congelar** antes de iniciar um armazenamento de instantâneo de consistência tooguarantee (consulte [xfs\_freeze(8) - man do Linux página](https://linux.die.net/man/8/xfs_freeze) para obter detalhes sobre **xfs\_congelar**).

tópico de saudação de consistência se torna ainda mais desafiador em um caso em que um único sistema de arquivos se estender por vários discos/volumes. Por exemplo, ao usar mdadm ou LVM e distribuição. Olá nota da SAP mencionados acima estados:

_&quot;Mas tenha em mente que o sistema de armazenamento de saudação terá consistência tooguarantee e/s ao criar um instantâneo de armazenamento por volume de dados do SAP HANA, ou seja, o instantâneo de um volume de dados específico ao serviço do SAP HANA deve ser uma operação atômica.&quot;_

Supondo que não há um sistema de arquivos XFS abrangência quatro discos virtuais do Azure, hello etapas a seguir fornecem um instantâneo consistente que representa a área de dados do HANA hello:

- Preparação do instantâneo do HANA
- Congelar o sistema de arquivos da saudação (por exemplo, use **xfs\_congelar**)
- Crie todos os instantâneos de blob necessários no Azure
- Descongelar o sistema de arquivos de saudação
- Confirme o instantâneo do HANA Olá

Recomendação é toouse Olá procedimento acima toobe de todos os casos no lado seguro hello, não importa qual sistema de arquivos. Ou, se for um disco único ou distribuição, via mdadm ou LVM em vários discos.

Ele é importante tooconfirm Olá HANA instantâneo. Vencimento toohello &quot;Copy-on-Write,&quot; SAP HANA podem não exigir espaço em disco adicional enquanto neste modo de preparação de instantâneo. &#39; s também não é possível toostart novos backups até que o instantâneo do SAP HANA Olá for confirmado.

Serviço de Backup do Azure usa tootake de extensões de VM do Azure respeito a consistência do sistema de arquivo hello. Essas extensões de VM não estão disponíveis para uso independente. Ainda assim é toomanage consistência de SAP HANA. Consulte o artigo relacionado Olá [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md) para obter mais informações.

### <a name="sap-hana-backup-scheduling-strategy"></a>Estratégia de agendamento de backup do SAP HANA

artigo do SAP HANA Olá [planejar sua estratégia de Backup e recuperação](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) estados a basic planejar toodo backups:

- Realize um instantâneo do armazenamento (diariamente)
- Faça um backup completo de dados usando o arquivo ou formato bacint (uma vez por semana)
- Backups de log automático

Opcionalmente, é possível não realizar nenhum instantâneo de armazenamento; eles podem ser substituídos por backups de delta do HANA, como backups incrementais ou diferenciais (consulte [Backups Delta](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Guia de administração do HANA Olá fornece uma lista de exemplos. Sugere que um ponto de recuperação SAP HANA tooa específico usando Olá sequência de backups a seguir:

1. Backup de dados completo
2. Backup diferencial
3. Backup incremental 1
4. Backup incremental 2
5. Backups de log

Sobre uma agenda exata como toowhen e a frequência com que um tipo específico de backup deve ocorrer, não é possível toogive uma diretriz geral, é muito específicas do cliente e depende de quantas alterações de dados ocorrerem no sistema de saudação. Uma recomendação básico do lado do SAP, que pode ser visto como orientação geral, é um backup HANA completo toomake uma vez por semana.
Sobre backups de log, consulte a documentação do SAP HANA Olá [Backups de Log](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP também recomenda a limpeza de saudação catálogo de backup tookeep ele cresça infinitamente (consulte [de limpeza para o catálogo de Backup e armazenamento de Backup](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>Arquivos de configuração do SAP HANA

Conforme indicado na hello mais frequentes [SAP Observação 1642148](https://launchpad.support.sap.com/#/notes/1642148), arquivos de configuração do SAP HANA Olá não fazem parte de um backup do HANA padrão. Eles não são essencial toorestore um sistema. configuração do HANA Olá pode ser alterada manualmente após a restauração de saudação. No caso de você desejar tooget Olá a mesma configuração personalizada durante o processo de restauração Olá, é necessário tooback backup de arquivos de configuração do HANA Olá separadamente.

Se backups HANA padrão tooa dedicado de sistema de arquivos de backup do HANA, um também pode copiar Olá toohello de arquivos de configuração mesmo sistema de arquivos de backup e, em seguida, copiar tudo como o destino final de armazenamento de toohello juntos interessantes armazenamento de blob.

### <a name="sap-hana-cockpit"></a>Ferramenta Cockpit do SAP HANA

SAP HANA Cockpit oferece a possibilidade de saudação do monitoramento e gerenciamento do SAP HANA por meio de um navegador. Ele também permite a manipulação de backups do SAP HANA e, portanto, pode ser usado como uma alternativa tooSAP Studio HANA e ABAP DBACOCKPIT (consulte [SAP HANA Cockpit](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) para obter mais informações).

![Esta figura mostra Olá tela de administração de banco de dados do SAP HANA Cockpit](media/sap-hana-backup-guide/image004.png)

Esta figura mostra Olá tela de administração de banco de dados do SAP HANA Cockpit e bloco backup Olá Olá à esquerda. Bloco de backup Olá vendo requer permissões de usuário apropriado para a conta de logon.

![Os backups podem ser monitorados na Ferramenta Cockpit do SAP HANA enquanto eles estiverem em andamento](media/sap-hana-backup-guide/image005.png)

Os backups podem ser monitorados na ferramenta cockpit da SAP HANA enquanto estiverem em andamento e, depois que ele for concluído, todos os detalhes de backup Olá estão disponíveis.

![Um exemplo usando o Firefox em uma VM do Azure SLES 12 com área de trabalho Gnome](media/sap-hana-backup-guide/image006.png)

Olá capturas de tela anteriores foram feitas a uma VM do Windows Azure. Esse é um exemplo usando o Firefox em uma VM do Azure SLES 12 com área de trabalho Gnome Ele mostra os agendamentos de backup do hello opção toodefine SAP HANA na ferramenta cockpit da SAP HANA. Como um também pode ver, sugere data/hora como um prefixo Olá dos arquivos de backup. No Studio do HANA SAP, o prefixo de padrão de saudação é &quot;concluir\_dados\_BACKUP&quot; ao fazer um backup de arquivo completo. É recomendável usar um prefixo exclusivo.

### <a name="sap-hana-backup-encryption"></a>Criptografia de backup do SAP HANA

O SAP HANA oferece criptografia de dados e de log. Se o log e dados do SAP HANA não são criptografados, em seguida, backups Olá também não são criptografados. É o toohello cliente toouse alguma forma de backups do solução de terceiros tooencrypt Olá SAP HANA. Consulte [dados e a criptografia de Volume de Log](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind mais informações sobre a criptografia do SAP HANA.

No Microsoft Azure, um cliente pode usar Olá IaaS VM tooencrypt de recurso de criptografia. Por exemplo, um pode usar dados dedicados de discos anexados toohello VM, que são usado toostore backups do SAP HANA, fazer cópias desses discos.

Serviço de Backup do Azure pode lidar com VMs/discos criptografados (consulte [como tooback backup e restauração criptografada máquinas virtuais com o Azure Backup](../../../backup/backup-azure-vms-encryption.md)).

Outra opção seria toomaintain Olá SAP HANA VM e seus discos sem criptografia e armazenar arquivos de backup Olá SAP HANA em uma conta de armazenamento para o qual a criptografia foi habilitada (consulte [criptografia de serviço de armazenamento do Azure para dados em repouso](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Configuração de teste

### <a name="test-virtual-machine-on-azure"></a>Teste da máquina virtual no Azure

Uma instalação do SAP HANA em uma VM do Azure GS5 foi usada para Olá testes de backup/restauração a seguir.

![Esta figura mostra a parte da saudação visão geral do portal do Azure para a VM de teste HANA Olá](media/sap-hana-backup-guide/image007.png)

Esta figura mostra a parte da saudação visão geral do portal do Azure para a VM de teste HANA hello.

### <a name="test-backup-size"></a>Teste do tamanho do backup

![Esta figura foi retirada do console de backup Olá no Studio HANA e mostra o tamanho do arquivo de backup Olá 229 GB para o servidor de índice do HANA Olá](media/sap-hana-backup-guide/image008.png)

Uma tabela fictícia foi preenchida com dados tooget um tamanho total dos dados de backup mais de 200 GB tooderive realista de dados de desempenho. Figura Olá foi retirada do console de backup Olá no Studio HANA e mostra o tamanho do arquivo de backup Olá 229 GB para o servidor de índice do HANA hello. Para testes de hello, o prefixo "COMPLETE_DATA_BACKUP" no SAP HANA Studio do backup de padrão de saudação foi usado. Em sistemas de produção real, um prefixo mais útil deve ser definido. A Ferramenta Cockpit da SAP HANA sugere a data/hora.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Toocopy da ferramenta de teste diretamente arquivos tooAzure armazenamento

arquivos de backup SAP HANA de tootransfer ferramenta de blobxfer de saudação diretamente o armazenamento de blob tooAzure ou compartilhamentos de arquivos do Azure, foi usada porque ele oferece suporte a destinos e ele podem ser facilmente integrados em scripts de automação de interface de linha de comando tooits de conclusão. Olá blobxfer ferramenta está disponível em [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Teste a estimativa de tamanho do backup

É importante tooestimate tamanho do backup saudação do SAP HANA. Essa estimativa ajuda tooimprove desempenho definindo o tamanho de arquivo máximo de backup Olá para um número de arquivos de backup, vencimento tooparallelism durante a cópia de um arquivo. (Esses detalhes são explicados mais adiante neste artigo.) Você também deve decidir se toodo completo de backup ou um delta de backup (incremental ou diferencial).

Felizmente, há uma instrução SQL simples que calcula o tamanho de Olá Olá dos arquivos de backup: **selecione \* de M\_BACKUP\_tamanho\_estimativas** (consulte [ Saudação de estimativa espaço necessário no hello sistema de arquivos para um Backup de dados](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![saída de Hello dessa instrução SQL corresponde quase Olá tamanho real do backup de dados completo Olá no disco](media/sap-hana-backup-guide/image009.png)

Para o sistema de teste hello, a saída de hello dessa instrução SQL corresponde quase Olá tamanho real do backup de dados completo Olá no disco.

### <a name="test-hana-backup-file-size"></a>Teste o tamanho do arquivo de backup do HANA

![console de backup do Hello HANA Studio permite que um tamanho de arquivo máximo Olá toorestrict HANA dos arquivos de backup](media/sap-hana-backup-guide/image010.png)

console backup do HANA Studio Olá permite que um tamanho de arquivo máximo Olá toorestrict HANA dos arquivos de backup. No ambiente do exemplo hello, esse recurso torna possível tooget backup menor vários arquivos em vez de um arquivo de backup de 230-GB. Menor tamanho do arquivo tem um impacto significativo no desempenho (consulte o artigo relacionado Olá [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Resumo

Com base nos resultados de teste de Olá Olá tabelas a seguir mostra os prós e contras das soluções tooback backup de um banco de dados do SAP HANA em execução em máquinas virtuais do Azure.

**Fazer backup de cópia e sistema de arquivos do SAP HANA toohello arquivos de backup depois toohello destino de backup final**

|Solução                                           |Prós                                 |Contras                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Mantém os backups do HANA em discos de VM                      |Nenhum trabalho de gerenciamento adicional     |Consome espaço em disco da VM local           |
|Armazenamento de tooblob Blobxfer ferramenta toocopy arquivos de backup |Paralelismo toocopy vários arquivos, armazenamento de blob moderado toouse opção | Manutenção de ferramenta adicional e scripts personalizados | 
|Cópia de blob por meio do Powershell ou CLI                    |Nenhuma ferramenta adicional necessária, pode ser realizada por meio do Azure Powershell ou CLI |processo manual, o cliente tem tootake respeito scripts e gerenciamento de blobs copiados para restauração|
|Compartilhamento de cópia de tooNFS                                  |Pós-processamento de arquivos de backup em outra VM sem impacto no servidor do HANA Olá|Processo de cópia lento|
|Blobxfer cópia tooAzure serviço de arquivos                |Não consome espaço nos discos VM locais|Sem suporte direto para gravação para backup do HANA, restrição de tamanho do compartilhamento de arquivos no momento em 5 TB|
|Agente de Backup do Azure                                 | Seria a melhor solução         | Não disponível no momento no Linux    |



**Backup do SAP HANA baseado em instantâneos de armazenamento**

|Solução                                           |Prós                                 |Contras                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Serviço de Backup do Azure                               | Permite o backup da VM com base em instantâneos de blob | Quando não usar a restauração no nível de arquivo, ele exige a criação de saudação de uma nova VM para o processo de restauração hello, o que implica, em seguida, a necessidade de saudação de uma nova chave de licença do SAP HANA|
|Instantâneos de blob manual                              | Flexibilidade toocreate e restauração específicos discos de VM sem alterar Olá ID exclusiva do VM|Todo trabalho manual, que tem toobe feita pelo cliente Olá|

## <a name="next-steps"></a>Próximas etapas
* [SAP HANA Azure Backup em nível de arquivo](sap-hana-backup-file-level.md) descreve a opção de backup baseado em arquivo hello.
* [Backup do HANA SAP com base em instantâneos de armazenamento](sap-hana-backup-storage-snapshots.md) descreve Olá armazenamento baseado em instantâneo opção de backup.
* toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md).
