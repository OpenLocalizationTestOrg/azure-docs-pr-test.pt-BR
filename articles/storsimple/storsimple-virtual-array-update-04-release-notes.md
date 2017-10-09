---
title: "Notas de versão 0,4 de atualização de matriz Virtual de aaaStorSimple | Microsoft Docs"
description: "Descreve abrir crítico problemas e resoluções para a execução de matriz Virtual StorSimple Olá atualizar 0,4."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>Notas de versão da Atualização 0.4 da StorSimple Virtual Array

## <a name="overview"></a>Visão geral

Olá notas de versão a seguir identificam problemas abertos críticos de saudação e Olá problemas resolvidos para atualizações do Microsoft Azure StorSimple Virtual Array.

Notas de versão de saudação são continuamente atualizadas, e que forem descobertas questões importantes que exijam uma solução alternativa, elas são adicionadas. Antes de implantar sua matriz Virtual StorSimple, revise atentamente informações Olá contidas nas notas de versão de saudação.

Atualização 0,4 corresponde a versão do software toohello **10.0.10289.0**.

> [!NOTE]
> As atualizações causam interrupção e reiniciam seu dispositivo. Se a e/s estão em andamento, o dispositivo Olá incorre em tempo de inatividade.


## <a name="whats-new-in-hello-update-04"></a>O que há de novo no hello atualização 0,4
A atualização 0.4 é principalmente uma compilação de correção de bug juntamente com algumas melhorias. Nesta versão, vários bugs, resultando em falhas de backup na versão anterior do hello foram resolvidos. correções de bug e aperfeiçoamentos principal Olá são da seguinte maneira:

- **Aprimoramentos de desempenho de backup** -nesta versão fez vários aprimoramentos importantes desempenho do backup tooimprove hello. Como resultado, backups de saudação que envolvem um grande número de arquivos Consulte uma redução significativa na toocomplete de tempo de saudação, para backups completos e incrementais.

- **Restauração desempenho aprimorado** -nesta versão contém aprimoramentos melhorar significativamente o desempenho de restauração de saudação ao usar um grande número de arquivos. Se usar 2-4 milhões de arquivos, é recomendável que você forneça uma matriz virtual com melhorias de saudação de toosee 16 GB RAM. Quando usar menos de 2 milhões de arquivos, requisito mínimo para a máquina virtual de saudação de Olá continua toobe 8 GB de RAM.

- **Pacote de tooSupport melhorias** -melhorias Olá incluem o log nas estatísticas de saudação de disco, CPU, memória, rede e nuvem no pacote de suporte hello, melhorando o processo de saudação do diagnóstico/depuração de problemas do dispositivo.

- **Limite localmente fixados iSCSI volumes too200 GB** -para volumes fixados localmente, é recomendável que você limite o volume iSCSI tooa 200 GB no StorSimple Virtual Array. reserva de local de saudação para volumes em camadas continua toobe 10% da saudação provisionado o tamanho do volume, mas está limitado a 200 GB. 

- **Correções de bugs relacionadas a backup** -em versões anteriores do software, havia problemas toobackups relacionados que possam causar falhas de backup. Esses bugs foram resolvidos nesta versão.


## <a name="issues-fixed-in-hello-update-04"></a>Problemas corrigidos Olá atualização 0,4

Olá tabela a seguir fornece um resumo dos problemas corrigidos nesta versão.

| Não. | Recurso | Problema |
| --- | --- | --- |
| 1 |Desempenho do backup|Olá versões anteriores, envolvendo um grande número de arquivos de backups de saudação levar um longo tempo toocomplete (na ordem de saudação de dias). Nesta versão, Olá completo e backups incrementais consulte uma redução significativa na Olá toocompletion de tempo. |
| 2 |Pacote de suporte|Disco, CPU, memória, rede e estatísticas de nuvem agora são registradas nos logs de suporte de toohello tornando os pacotes de suporte de saudação muito eficiente na solução de problemas no dispositivo.|
| 3 |Backup |Em versões anteriores, os backups de longa execução pode resultar em uma situação de espaço no dispositivo Olá resultando em falhas de backup. Esse erro é abordado nesta versão, permitindo que os backups não mais de 5 tooqueue ao mesmo tempo.|
| 4 |iSCSI | Em versões anteriores, a reserva local Olá para volumes fixados localmente ou em camadas foi 10% do tamanho do volume Olá provisionado. Nesta versão, a reserva local Olá para todos os volumes de iSCSI (localmente afixado ou em camadas) é % too10 limitado com um máximo de até 200 GB (para volumes em camadas maiores que 2 TB), assim, liberar mais espaço no disco local hello. É recomendável volumes Olá localmente afixado nesta versão seja limitado too200 GB.|


## <a name="known-issues-in-hello-update-04"></a>Problemas conhecidos no hello atualização 0,4

Olá tabela a seguir fornece um resumo dos problemas conhecidos Olá matriz Virtual do StorSimple e inclui os problemas de saudação observado na versão de versões anteriores do hello. 

| Não. | Recurso | Problema | Solução alternativa/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais de saudação criados na versão de visualização de saudação não podem ser atualizada tooa suporte para versão de disponibilidade geral. |Esses dispositivos virtuais devem fazer failover para Olá versão disponibilidade geral usando um fluxo de trabalho de recuperação de desastres. |
| **2.** |Disco de dados provisionado |Uma vez que você possua um disco de dados de um determinado tamanho especificado e criar dispositivo virtual do hello correspondente StorSimple, você deve não expandir ou reduzir Olá disco de dados. Tentativa de resultados de toodo em uma perda de todos os dados de saudação nas camadas de local de saudação do dispositivo hello. | |
| **3.** |Política de grupo |Quando um dispositivo está ingressado no domínio, aplicar uma política de grupo pode afetar a operação de dispositivo hello. |Certifique-se de que sua matriz virtual está em sua própria unidade organizacional (UO) do Active Directory e nenhum objeto de diretiva de grupo (GPO) é aplicada tooit. |
| **4.** |Interface do Usuário da Web local |Se os recursos de segurança aprimorados estão habilitados no Internet Explorer (IE ESC), algumas páginas da interface do usuário da Web local, como Solução de Problemas ou Manutenção, podem não funcionar corretamente. Os botões nessas páginas também podem não funcionar. |Desligue os recursos de segurança reforçada do Internet Explorer. |
| **5.** |Interface do Usuário da Web local |Em uma máquina virtual de Hyper-V, Olá interfaces de rede na web hello interface do usuário são exibidos como interfaces de 10 Gbps. |Esse comportamento é um reflexo do Hyper-V. O Hyper-V sempre mostra 10 Gbps para adaptadores de rede virtual. |
| **6.** |Compartilhamentos ou volumes em camadas |Não há suporte para o intervalo de bytes de bloqueio para aplicativos que funcionam com hello StorSimple volumes em camadas. Se o bloqueio de intervalo de bytes estiver habilitado, a disposição em camadas do StorSimple não funcionará. |As medidas recomendadas incluem:  <br></br>Desligar o bloqueio de intervalo de bytes em sua lógica de aplicativo.<br></br>Escolha dados tooput para este aplicativo em volumes localmente afixados contrário como volumes de tootiered.<br></br>*Limitação*: quando usar localmente fixados volumes e bloqueio de intervalo de bytes é habilitado, volume Olá fixado localmente pode ser online antes mesmo de saudação restauração for concluída. Nesses casos, se uma restauração está em andamento, em seguida, você deve aguardar Olá toocomplete de restauração. |
| **7.** |Compartilhamentos em camadas |Trabalhar com arquivos grandes pode resultar em uma divisão em camadas lenta. |Ao trabalhar com arquivos grandes, é recomendável que esse arquivo maior Olá é menor do que 3% do tamanho do compartilhamento de saudação. |
| **8.** |Capacidade utilizada para compartilhamentos |Você pode ver compartilhar consumo quando não há nenhum dado no compartilhamento de saudação. Isso ocorre porque a capacidade de saudação usada para compartilhamentos inclui metadados. | |
| **9.** |Recuperação de desastre |Você só pode executar a recuperação de desastres de saudação de um toohello de servidor de arquivo mesmo domínio que o dispositivo de origem hello. Não há suporte para o dispositivo de destino de tooa de recuperação de desastres em outro domínio nesta versão. |Isso será implementado em uma versão posterior. |
| **10.** |Azure PowerShell |os dispositivos virtuais StorSimple Olá não podem ser gerenciados por meio de saudação do PowerShell do Azure nesta versão. |Todo o gerenciamento de saudação de dispositivos virtuais Olá deve ser feito por meio de hello portal clássico do Azure e a interface da web local hello. |
| **11.** |Alteração de senha |console de dispositivo virtual array Olá só aceita entrada no formato de teclado en-US. | |
| **12.** |CHAP |Não é possível remover as credenciais CHAP depois de criadas. Além disso, se você modificar as credenciais CHAP Olá, precisa de volumes de saudação tootake offline e, em seguida, coloque-os online para Olá alterar tootake efeito. |Esse problema será corrigido em uma versão futura. |
| **13.** |Servidor iSCSI |Olá 'Usado armazenamento' exibido para um volume iSCSI pode ser diferente no serviço do StorSimple Manager hello e host iSCSI de saudação. |host de iSCSI Olá tem o modo de exibição de sistema de arquivos de hello.<br></br>dispositivo Olá vê blocos Olá distribuídos ao volume Olá estava no tamanho máximo de saudação. |
| **14.** |Servidor de arquivos |Se um arquivo em uma pasta tiver um fluxo de dados alternativo (ADS) associado a ele, Olá anúncios não é copiado ou restaurado por meio de recuperação de desastres, clonagem e recuperação em nível de Item. | |
| **15.** |Servidor de arquivos |Não há suporte para links simbólicos. | |
| **16.** |Servidor de arquivos |Arquivos protegidos pelo Windows Encrypting File System (EFS) quando copiou ou armazenado em Olá resultado do servidor de arquivo de matriz Virtual do StorSimple em uma configuração sem suporte.  | |

## <a name="next-step"></a>Próxima etapa
[Instale a atualização 0.4](storsimple-virtual-array-install-update-04.md) em sua StorSimple Virtual Array.

## <a name="references"></a>Referências
Procurando uma nota de versão mais antiga? Acesse: 

* [Notas de versão da atualização 0.3 da StorSimple Virtual Array](storsimple-ova-update-03-release-notes.md)
* [Notas de versão as Atualizações 0.1 e 0.2 do StorSimple Virtual Array](storsimple-ova-update-01-release-notes.md)
* [Notas de versão de disponibilidade geral do StorSimple Virtual Array](storsimple-ova-pp-release-notes.md)

