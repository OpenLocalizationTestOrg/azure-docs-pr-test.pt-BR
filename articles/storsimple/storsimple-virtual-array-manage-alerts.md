---
title: aaaView e gerenciar alertas do Microsoft Azure StorSimple Virtual Array | Microsoft Docs
description: "Descreve condições de alerta de matriz Virtual do StorSimple e severidade e como Olá toouse StorSimple Manager toomanage alertas de serviço."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Use o Gerenciador de dispositivo StorSimple toomanage alertas para Olá matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

recurso de alertas de Olá Olá serviço do Gerenciador de dispositivos de StorSimple fornece uma maneira para você tooreview e limpar os alertas relacionados tooStorSimple Virtual matrizes em tempo real. Você pode usar alertas Olá Olá **resumo serviço** toocentrally folha monitorar Olá problemas de integridade de suas matrizes de Virtual do StorSimple e Olá solução geral do Microsoft Azure StorSimple.

Este tutorial descreve como os níveis de severidade de alerta de notificações de alerta tooconfigure, condições de alerta comuns e como tooview e rastrear os alertas. Além disso, ele inclui alerta referência rápida de localizar um alerta específico de tabelas, que permitem que você tooquickly e respondem adequadamente.

![Página de alertas](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Definição de configurações de alerta

Você pode escolher se deseja toobe notificado por email Olá das condições de alerta para cada uma das suas matrizes de Virtual do StorSimple. Além disso, você pode identificar outros destinatários de notificação de alerta, digitando seus endereços de email no hello **destinatários de email adicionais** caixa, separados por ponto e vírgula.

> [!NOTE]
> Você pode inserir um máximo de 20 endereços de email por matriz virtual.


Depois de habilitar notificação por email para uma matriz virtual, os membros da lista de notificação de saudação receberão uma mensagem de email sempre que ocorrer um alerta crítico. mensagens de saudação serão enviadas por  *storsimple-alerts-noreply@mail.windowsazure.com*  e descreverão a condição de alerta de saudação. Destinatários podem clicar em **Unsubscribe** tooremove si na lista de notificação de email hello.

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable notificação por email para alertas

1. Vá tooyour Gerenciador de dispositivos de StorSimple, serviço e no hello **gerenciamento** seção, selecione e clique em **dispositivos**. Na lista de saudação de dispositivos exibida, selecione e clique em seu dispositivo.
   
    ![Configurações de alerta](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Isso abre a saudação **configurações** folha. Em Olá **configurações do dispositivo** seção, selecione **geral**. Isso abre a saudação **configurações gerais** folha.
   
    ![configuração da notificação de alertas](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. Em Olá **configurações gerais** folha, ir muito**configurações de alerta** seção e defina Olá seguinte:
   
   1. Em Olá **habilitar notificação de email** campo, selecione **Sim**.
   2. Em Olá **administradores de serviço de Email** campo, selecione **Sim** se desejar que o administrador de serviço toohave hello e todos os administradores recebam notificações de alerta de saudação.
   3. Em Olá **destinatários de email adicionais** , digite os endereços de email de saudação de todos os outros destinatários que devem receber notificações de alerta de saudação. Insira os nomes no formato de saudação  *someone@somewhere.com* . Use endereços de email de saudação de tooseparate ponto e vírgula. Você pode configurar um máximo de 20 endereços de email por dispositivo virtual.
      
       ![configuração da notificação de alertas](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend uma notificação de email de teste, clique em **enviar email de teste**. saudação de serviço do Gerenciador de dispositivos de StorSimple exibirá mensagens de status conforme ele encaminha a notificação de teste de saudação.
      
       ![Email de notificação de teste de alertas enviado](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Se o teste de saudação mensagem de notificação não serão enviados, serviço de Gerenciador de dispositivos de StorSimple Olá exibirá uma mensagem apropriada. Clique em **Okey**, aguarde alguns minutos e, em seguida, tente toosend a mensagem de notificação de teste novamente.
      > 
      > 
   5. Final Olá Olá página, clique em **salvar** toosave sua configuração. Quando solicitado a confirmar, clique em **Sim**.
      
      ![Email de notificação de teste de alertas enviado](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Condições comuns de alerta

A matriz de Virtual do StorSimple gera alertas em variedade de tooa de resposta de condições. Olá seguem tipos mais comuns de saudação das condições de alerta:

* **Problemas de conectividade** – esses alertas ocorrem quando há dificuldade na transferência de dados. Problemas de comunicação podem ocorrer durante a transferência de dados tooand de vencimento ou conta de armazenamento do Azure Olá toolack de conectividade entre dispositivos virtuais hello e serviço de Gerenciador de dispositivos de StorSimple hello. Problemas de comunicação são alguns dos toofix mais difícil Olá porque há muitos pontos de falha. Sempre, primeiro você deve verificar se a conectividade de rede e acesso à Internet estão disponíveis antes de continuar toomore a solução de problemas avançada. Para obter informações sobre portas e configurações de firewall, vá muito[requisitos de sistema de matriz Virtual StorSimple](storsimple-ova-system-requirements.md). Para obter ajuda com solução de problemas, vá muito[solução de problemas com o cmdlet Olá Conexão de teste](storsimple-troubleshoot-deployment.md).
* **Problemas de desempenho** – esses alertas são causados quando o sistema não estiver sendo executado corretamente, como quando ele está sob uma carga pesada.

Além disso, você pode ver toosecurity relacionados de alertas, atualizações ou falhas no trabalho.

## <a name="alert-severity-levels"></a>Níveis de severidade do alerta

Alertas têm diferentes níveis de severidade, dependendo do impacto Olá Olá situação de alerta terá e Olá a necessidade de um alerta de toohello de resposta. níveis de severidade de saudação são:

* **Crítico** – este alerta está em condição de tooa de resposta que está afetando o desempenho adequado de saudação do seu sistema. Ação é necessário tooensure que o serviço do StorSimple Olá não seja interrompido.
* **Aviso** – essa condição poderá se tornar crítica se não for resolvida. Você deve investigar a situação hello e tomar qualquer problema de saudação tooclear ação é necessária.
* **Informações** – esse alerta contém informações que podem ser úteis para controlar e gerenciar seu sistema.

## <a name="view-and-track-alerts"></a>Exibir e controlar os alertas

lâmina do resumo de serviço do Gerenciador de dispositivos do StorSimple Olá fornece uma visão geral rápida número Olá de alertas em seus dispositivos virtuais, organizados por nível de severidade.

![Painel de alertas](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Clique em Olá Olá de tooopen nível de severidade **alertas** folha. resultados da saudação incluem apenas os alertas de saudação que correspondem a esse nível de severidade.

![Relatório de alertas no escopo do tipo tooalert](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Clique em um alerta em detalhes adicionais do hello lista tooget alerta hello, incluindo Olá hora da última Olá alerta foi relatado, número de saudação de ocorrências de saudação alerta no dispositivo Olá e Olá ação recomendada tooresolve hello.

![Lista de alertas e detalhes](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Você pode copiar o arquivo de texto em tooa Olá detalhes do alerta se você precisar toosend Olá informações tooMicrosoft suporte. Após ter seguido recomendação Olá e resolver Olá condição de alerta local, você deve limpar o alerta de saudação da lista de saudação. Selecione alerta Olá Olá lista e, em seguida, clique em **limpar**. tooclear vários alertas, selecionadas cada alerta, clique em qualquer coluna exceto Olá **alerta** coluna e clique **limpar** após você ter selecionado todos Olá toobe alertas desmarcada.

Quando você clica em **limpar**, você terá Olá oportunidade tooprovide comentar alerta hello e etapas de saudação que levou tooresolve Olá problema. 

![comentários de alerta](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Alguns eventos serão apagados pelo sistema Olá se outro evento for acionado com novas informações. 

## <a name="sort-and-review-alerts"></a>Classificação e análise de alertas

Olá **alertas** folha pode exibir os alertas de too250. Se você excedeu o número de alertas, nem todos os alertas serão exibidos no modo de exibição do saudação padrão. Você pode combinar Olá campos toocustomize quais alertas são exibidas a seguir:

* **Status** – Você pode exibir alertas **Ativos** ou **Removidos**. Alertas ativos ainda estão sendo acionados no seu sistema, enquanto os alertas apagados tenham sido apagadas manualmente por um administrador ou desmarcadas programaticamente porque sistema Olá atualizado condição de alerta de saudação com novas informações.
* **Severidade** – Você pode exibir alertas de todos os níveis de severidade (críticos, avisos, informações) ou apenas uma determinada severidade, como, por exemplo, somente alertas críticos.
* **Origem** – você pode exibir alertas de todas as fontes ou limitar Olá alertas toothose que vêm de um serviço de saudação ou ou Olá a todos os dispositivos virtuais.
* **Intervalo de tempo** – especificando Olá **de** e **para** datas e os carimbos de hora, você pode examinar alertas durante a saudação período de tempo que você está interessado.

## <a name="alerts-quick-reference"></a>Referência rápida de alertas

Olá tabelas a seguir lista alguns dos alertas de StorSimple Olá que você pode encontrar, bem como recomendações e informações adicionais quando disponíveis. Alertas de matriz Virtual StorSimple se encaixam em uma saudação categorias a seguir:

* [Alertas de conectividade de nuvem](#cloud-connectivity-alerts)
* [Alertas de configuração](#configuration-alerts)
* [Alertas de falha nos trabalhos](#job-failure-alerts)
* [Alertas de desempenho](#performance-alerts)
* [Alertas de segurança](#security-alerts)
* [Alertas de atualização](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertas de conectividade de nuvem

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Dispositivo  *<device name>*  está conectado não toohello nuvem. |Olá chamado dispositivo não pode se conectar a nuvem toohello. |Não foi possível conectar toohello nuvem. Isso pode ter ocorrido tooone seguinte hello:<ul><li>Pode haver um problema com as configurações de rede de saudação em seu dispositivo.</li><li>Pode haver um problema com as credenciais de conta de armazenamento hello.</li></ul>Para obter mais informações sobre solução de problemas de conectividade, acesse toohello [interface da web local](storsimple-ova-web-ui-admin.md) do dispositivo hello. |

### <a name="configuration-alerts"></a>Alertas de configuração

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Configuração do dispositivo virtual local sem suporte. |Desempenho lento. |configuração atual de saudação pode resultar em degradação do desempenho. Certifique-se de que o servidor atende aos requisitos mínimos de configuração de saudação. Para obter mais informações, vá muito[StorSimple Virtual Array requisitos](storsimple-ova-system-requirements.md). |
| Você está com pouco espaço em disco provisionado em <*nome do dispositivo*>. |Aviso de espaço em disco. |Você está com pouco espaço em disco provisionado. toofree espaço, considere mover cargas de trabalho tooanother volume ou compartilhamento ou excluir dados. |

### <a name="job-failure-alerts"></a>Alertas de falha nos trabalhos

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| O backup de <*nome do dispositivo*> não pôde ser concluído. |Falha no trabalho de backup. |Não foi possível criar um backup. Considere uma das seguintes hello:<ul><li>Problemas de conectividade podem estar impedindo a operação de backup Olá seja concluída com êxito. Certifique-se de que não haja nenhum problema de conectividade. Para obter mais informações sobre solução de problemas de conectividade, acesse toohello [interface da web local](storsimple-ova-web-ui-admin.md) para seu dispositivo virtual.</li><li>Você atingiu o limite de armazenamento disponível hello. toofree espaço, considere a exclusão de todos os backups que não são mais necessários.</li></ul> Resolver problemas de hello, desmarque o alerta hello e repita a operação de saudação. |
| A clonagem de <*nome do dispositivo*> não pôde ser concluída. |Falha no trabalho de clonagem. |Não foi possível criar um clone. Considere uma das seguintes hello:<ul><li>sua lista de backup pode não ser válida. Atualize Olá lista tooverify ainda seja válido.</li><li>Problemas de conectividade podem estar impedindo a operação de clonagem Olá seja concluída com êxito. Certifique-se de que não haja nenhum problema de conectividade.</li><li>Você atingiu o limite de armazenamento disponível hello. toofree espaço, considere a exclusão de todos os backups que não são mais necessários.</li></ul>Resolver problemas de hello, desmarque o alerta hello e repita a operação de saudação. |

### <a name="performance-alerts"></a>Alertas de desempenho

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Você está sofrendo atrasos inesperados na transferência de dados. |Transferência de dados lenta. |Erros de restrição ocorrem ao exceder os destinos de escalabilidade de saudação de um serviço de armazenamento. serviço de armazenamento de saudação faz essa tooensure que nenhum cliente único ou Locatário pode usar o serviço de saudação à custa de saudação de outras pessoas. Para obter mais informações sobre como solucionar problemas de sua conta de armazenamento do Azure, vá muito[monitorar, diagnosticar e solucionar problemas de armazenamento do Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Há pouco espaço local de reserva em disco no <*nome do dispositivo*>. |Tempo de resposta lento. |total de 10% da saudação tamanho provisionado para <*nome do dispositivo*> é reservado no hello dispositivo local e que você esteja agora Olá com pouco espaço reservado. carga de trabalho de saudação em <*nome do dispositivo*> está gerando uma maior taxa de variação ou você pode ter migrado recentemente uma grande quantidade de dados. Isso pode resultar em desempenho reduzido. Considere uma disso Olá tooresolve ações a seguir:<ul><li>Aumente Olá nuvem largura de banda toothis dispositivo.</li><li>Reduza ou mova cargas de trabalho tooanother volume ou compartilhamento.</li></ul> |

### <a name="security-alerts"></a>Alertas de segurança

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| A senha de <*nome do dispositivo*> expirará em <*número*> dias. |Aviso de senha. |Sua senha expirará em < número> dias. Considere alterar sua senha. Para obter mais informações, vá muito[senha de administrador do dispositivo do alteração Olá matriz Virtual StorSimple](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Alertas de atualização

| Texto de alerta | Evento | Mais informações / ações recomendadas |
|:--- |:--- |:--- |
| Novas atualizações estão disponíveis para seu dispositivo. |Atualizações toohello matriz Virtual StorSimple estão disponíveis. |Você pode instalar novas atualizações da saudação **manutenção** página. |
| Não foi possível verificar novas atualizações do <*nome do dispositivo*>. |Falha de atualização. |Ocorreu um erro durante a instalação de novas atualizações. Você pode instalar manualmente as atualizações de saudação. Se Olá problema persistir, entre em contato com [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Próximas etapas

* [Saiba mais sobre Olá matriz Virtual StorSimple](storsimple-ova-overview.md).

