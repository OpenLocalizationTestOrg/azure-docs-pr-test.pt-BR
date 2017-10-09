---
title: "Notas de versão de atualizações de matriz Virtual aaaStorSimple | Microsoft Docs"
description: "Descreve as questões abertas fundamentais e as resoluções para Olá matriz Virtual StorSimple executar Update 0.2 e 0.1."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Notas de versão as Atualizações 0.1 e 0.2 do StorSimple Virtual Array
## <a name="overview"></a>Visão geral
Olá notas de versão a seguir identificam problemas abertos críticos de saudação e Olá problemas resolvidos para atualizações do Microsoft Azure StorSimple Virtual Array. (Microsoft Azure StorSimple Virtual Array é também conhecido como dispositivo virtual do hello StorSimple local ou o dispositivo virtual StorSimple hello.) 

Notas de versão de saudação são continuamente atualizadas, e que forem descobertas questões importantes que exijam uma solução alternativa, elas são adicionadas. Antes de implantar seu dispositivo virtual StorSimple, revise atentamente as informações de saudação contidas nas notas de versão de saudação.

Atualização 0,2 corresponde a versão do software toohello **10.0.10280.0**; Atualização de 0.1 é versão **10.0.10279.0**. seções de saudação abaixo lista as alterações de saudação para cada atualização. 

> [!NOTE]
> As atualizações causam interrupção e reiniciarão seu dispositivo. Se a e/s estão em andamento, dispositivo Olá incorrerá em tempo de inatividade.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemas corrigidos Olá atualização 0,2
Atualização de 0,2 inclui todas as alterações de atualização 0,1 na adição toohello corrija descrita em Olá a tabela a seguir:

| Recurso | Problema |
| --- | --- |
| Atualizações |Na versão mais recente Olá, atualizações não foram detectadas automaticamente no hello portal clássico do Azure, para que você tinha toouse Olá atualizações de tooinstall de interface de usuário da Web locais. Esse problema foi corrigido nesta versão. Depois de instalar a atualização 0,2, você pode instalar atualizações futuras usando Olá portal clássico do Azure. |

## <a name="whats-new-in-hello-update-01"></a>O que há de novo no hello atualização 0,1
Atualização 0,1 contém seguinte Olá correções e aprimoramentos. 

* **Maior flexibilidade para interrupções de nuvem**: esta versão contém várias correções de bug em torno de recuperação de desastre, backup, restauração e camadas no evento de saudação de uma interrupção de conectividade de nuvem. 
* **Melhor desempenho de restauração**: esta versão contém correções de bugs que têm significativamente reduzir o tempo de conclusão de saudação saudação de trabalhos de restauração.
* **Automatizada de otimização de reclamação de espaço**: quando dados são excluídos em volumes de provisionamento thin, hello blocos de armazenamento não utilizada necessário toobe recuperada. Nesta versão tem o processo de recuperação de espaço Olá aprimorado da nuvem Olá resultando em Olá não utilizado se tornando mais rápidas em comparação com como toohello versões anteriores disponíveis de espaço.
* **Novas imagens de disco virtual**: novo VHD e VHDX VMDK agora estão disponíveis via Olá portal clássico do Azure. Você pode baixar essas imagens tooprovision novos atualização 0,1 dispositivos.
* **Melhorar a precisão de saudação do status de trabalhos no portal de saudação**: no hello versão anterior do software, status de trabalho relatórios no portal de saudação não era granular. Esse problema foi corrigido nesta versão.
* **Experiência de junção de domínio**: correções de bugs relacionadas a junção toodomain e renomeação de dispositivo de saudação.

## <a name="issues-fixed-in-hello-update-01"></a>Problemas corrigidos Olá atualização 0.1
Olá tabela a seguir fornece um resumo dos problemas corrigidos nesta versão.

| Não. | Recurso | Problema |
| --- | --- | --- |
| 1 |VMDK |Em algumas versões do VMware, disco de SO Olá foi visto como esparso causando alertas e interromper as operações normais. Isso foi corrigido nesta versão. |
| 2 |Servidor iSCSI |Versão da última hello, usuário Olá foi toospecify necessário um gateway para cada interface de rede habilitado do seu dispositivo virtual StorSimple. Esse comportamento é alterado nesta versão para que o usuário hello tem tooconfigure pelo menos um gateway para todas as interfaces de rede Olá habilitado. |
| 3 |Pacote de suporte |Em Olá versão anterior do software, dar suporte à coleta de pacote falha quando o tamanho do pacote de saudação foi maior que 1 GB. Esse problema foi corrigido nesta versão. |
| 4 |Acesso à nuvem |Versão da última Olá, se hello matriz Virtual do StorSimple não tem conectividade de rede e foi reiniciado, hello UI local teria problemas de conectividade. Esse problema foi corrigido nesta versão. |
| 5 |Gráficos de monitoramento |Na versão anterior do hello, seguindo um failover de dispositivo, os gráficos de utilização de capacidade de nuvem Olá exibem valores incorretos em Olá portal clássico do Azure. Isso é corrigido na versão atual do hello. |

## <a name="known-issues-in-hello-update-01"></a>Problemas conhecidos no hello atualização 0.1
Olá tabela a seguir fornece um resumo dos problemas conhecidos Olá matriz Virtual do StorSimple e inclui os problemas de saudação observado na versão de versões anteriores do hello. **Olá versão problemas observado nesta versão são marcados com um asterisco. Quase todos os problemas de saudação nesta lista têm obtidas da versão Olá GA de matriz Virtual StorSimple.**

| Não. | Recurso | Problema | Solução alternativa/comentários |
| --- | --- | --- | --- |
| **1.** |Atualizações |dispositivos virtuais de saudação criados na versão de visualização de saudação não podem ser atualizada tooa suporte para versão de disponibilidade geral. |Esses dispositivos virtuais devem fazer failover para Olá versão disponibilidade geral usando um fluxo de trabalho de recuperação de desastres. |
| **2.** |Disco de dados provisionado |Uma vez que você possua um disco de dados de um determinado tamanho especificado e criar dispositivo virtual do hello correspondente StorSimple, você deve não expandir ou reduzir Olá disco de dados. Tentar toodo portanto resultará em perda de todos os dados de saudação nas camadas de local de saudação do dispositivo hello. | |
| **3.** |Política de grupo |Quando um dispositivo está ingressado no domínio, aplicar uma política de grupo pode afetar a operação de dispositivo hello. |Certifique-se de que sua matriz virtual está em sua própria unidade organizacional (UO) do Active Directory e nenhum objeto de diretiva de grupo (GPO) é aplicada tooit. |
| **4.** |Interface do Usuário da Web local |Se os recursos de segurança aprimorados estão habilitados no Internet Explorer (IE ESC), algumas páginas da interface do usuário da Web local, como Solução de Problemas ou Manutenção, podem não funcionar corretamente. Os botões nessas páginas também podem não funcionar. |Desligue os recursos de segurança reforçada do Internet Explorer. |
| **5.** |Interface do Usuário da Web local |Em uma máquina virtual de Hyper-V, Olá interfaces de rede na web hello interface do usuário são exibidos como interfaces de 10 Gbps. |Esse comportamento é um reflexo do Hyper-V. O Hyper-V sempre mostra 10 Gbps para adaptadores de rede virtual. |
| **6.** |Compartilhamentos ou volumes em camadas |Não há suporte para o intervalo de bytes de bloqueio para aplicativos que funcionam com hello StorSimple volumes em camadas. Se o bloqueio de intervalo de bytes estiver habilitado, a disposição em camadas do StorSimple não funcionará. |As medidas recomendadas incluem:  <br></br>Desligar o bloqueio de intervalo de bytes em sua lógica de aplicativo.<br></br>Escolha dados tooput para este aplicativo em volumes localmente afixados contrário como volumes de tootiered.<br></br>*Limitação*: se usando localmente fixados volumes e bloqueio de intervalo de bytes é habilitado, lembre-se de que volume Olá fixado localmente pode ser online antes mesmo de saudação restauração for concluída. Nesses casos, se uma restauração está em andamento, em seguida, você deve aguardar Olá toocomplete de restauração. |
| **7.** |Compartilhamentos em camadas |Trabalhar com arquivos grandes pode resultar em uma divisão em camadas lenta. |Ao trabalhar com arquivos grandes, é recomendável que esse arquivo maior Olá é menor do que 3% do tamanho do compartilhamento de saudação. |
| **8.** |Capacidade utilizada para compartilhamentos |Você pode ver compartilhar consumo na ausência de saudação de todos os dados no compartilhamento de saudação. Isso ocorre porque a capacidade de saudação usada para compartilhamentos inclui metadados. | |
| **9.** |Recuperação de desastre |Você só pode executar a recuperação de desastres de saudação de um toohello de servidor de arquivo mesmo domínio que o dispositivo de origem hello. Não há suporte para o dispositivo de destino de tooa de recuperação de desastres em outro domínio nesta versão. |Isso será implementado em uma versão posterior. |
| **10.** |Azure PowerShell |os dispositivos virtuais StorSimple Olá não podem ser gerenciados por meio de saudação do PowerShell do Azure nesta versão. |Todo o gerenciamento de saudação de dispositivos virtuais Olá deve ser feito por meio de hello portal clássico do Azure e a interface da web local hello. |
| **11.** |Alteração de senha |console de dispositivo virtual array Olá só aceita entrada no formato de teclado en-US. | |
| **12.** |CHAP |Não é possível remover as credenciais CHAP depois de criadas. Além disso, se você modificar as credenciais CHAP hello, será necessário tootake volumes de saudação offline e, em seguida, coloque-os online para Olá alterar tootake efeito. |Isso será corrigido em uma versão futura. |
| **13.** |Servidor iSCSI |Olá 'Usado armazenamento' exibido para um volume iSCSI pode ser diferente no serviço do StorSimple Manager hello e host iSCSI de saudação. |host de iSCSI Olá tem o modo de exibição de sistema de arquivos de hello.<br></br>dispositivo Olá vê blocos Olá distribuídos ao volume Olá estava no tamanho máximo de saudação. |
| **14.** |Servidor de arquivos* |Se um arquivo em uma pasta tiver um fluxo de dados alternativo (ADS) associado a ele, Olá anúncios não é copiado ou restaurado por meio de recuperação de desastres, clonagem e recuperação em nível de Item. | |

## <a name="next-step"></a>Próxima etapa
[Instale as Atualizações](storsimple-ova-install-update-01.md) em seu StorSimple Virtual Array.

