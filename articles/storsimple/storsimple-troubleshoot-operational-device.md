---
title: aaaTroubleshoot um dispositivo StorSimple implantado | Microsoft Docs
description: "Descreve como toodiagnose e corrigir erros que ocorrem em um dispositivo StorSimple que está sendo implantado e operacional."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Solucionar problemas de um dispositivo operacional do StorSimple
## <a name="overview"></a>Visão geral
Este artigo oferece orientações úteis de solução de problemas para resolver problemas de configuração que você poderá encontrar depois que seu dispositivo StorSimple estiver implantado e operacional. Descreve problemas comuns, possíveis causas e etapas recomendadas toohelp que resolver problemas que podem ocorrer quando você executa o Microsoft Azure StorSimple. Essas informações se aplicam a dispositivo físico tooboth Olá StorSimple local e o dispositivo virtual StorSimple hello.

Final Olá deste artigo, que você pode encontrar uma lista de códigos de erro que você pode encontrar durante a operação do Microsoft Azure StorSimple, bem como as etapas, você pode tomar tooresolve erros de saudação. 

## <a name="setup-wizard-process-for-operational-devices"></a>Processo do assistente de instalação de dispositivos operacionais
Use o Assistente de instalação hello ([Invoke-HcsSetupWizard][1]) toocheck Olá a configuração do dispositivo e tomar uma ação corretiva, se necessário.

Quando você executa o Assistente de instalação de saudação em um dispositivo anteriormente configurado e operacional, o fluxo de processo Olá é diferente. Você pode alterar somente Olá entradas a seguir:

* Endereço IP, máscara de sub-rede e gateway
* Servidor DNS primário
* Servidor NTP primário
* Configuração do proxy da Web opcional

Assistente de instalação de saudação não executa Olá operações relacionadas toopassword coleta e o registro do dispositivo.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Erros que ocorrem durante as execuções subsequentes do Assistente de instalação de saudação
Olá, a tabela a seguir descreve os erros de saudação que você pode encontrar ao executar o Assistente de instalação de saudação em um dispositivo operacional, possíveis causas de erros de Olá e as ações recomendadas tooresolve-los. 

| Não. | Mensagem ou condição de erro | Possíveis causas | Ação recomendada |
|:--- |:--- |:--- |:--- |
| 1 |Erro 350032: este dispositivo já foi desativado. |Você verá esse erro se você executar o Assistente de instalação de saudação em um dispositivo que está desativado. |[Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para as próximas etapas. Um dispositivo desativado não pode ser colocado em serviço. Uma redefinição de fábrica pode ser necessária antes de dispositivo Olá pode ser ativado novamente. |
| 2 |Invoke-HcsSetupWizard : ERROR_INVALID_FUNCTION(Exception from HRESULT: 0x80070001) |atualização do servidor DNS Hello está falhando. As configurações de DNS são configurações globais e são aplicadas em todas as interfaces de rede Olá habilitado. |Habilitar Olá interface e aplique as configurações de DNS Olá novamente. Isso pode afetar a rede Olá para outras interfaces habilitadas porque essas configurações são globais. |
| 3 |dispositivo Olá aparece toobe online no portal de serviço do StorSimple Manager hello, mas quando você tente toocomplete Olá a instalação mínima e salva a configuração de hello, operação Olá falha. |Durante a instalação inicial, Olá web proxy não foi configurado, mesmo se houvesse um servidor proxy real no lugar. |Saudação de uso [cmdlet Test-HcsmConnection] [ 2] toolocate erro de saudação. [Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) se você estiver toocorrect não é possível problema de saudação. |
| 4 |Invoke-HcsSetupWizard: O valor não recai no intervalo esperado de saudação. |Uma máscara de sub-rede incorreta gera esse erro. As possíveis causas são:  <ul><li> máscara de sub-rede Hello está ausente ou vazio.</li><li>formato de prefixo Ipv6 Hello está incorreto.</li><li>interface Hello está habilitado para a nuvem, mas o gateway hello está ausente ou incorreto.</li></ul>Observe que o DATA 0 é automaticamente habilitada para a nuvem se configurada por meio do Assistente de instalação de saudação. |problema de saudação toodetermine, use a subrede 0.0.0.0 ou 256.256.256.256 e, em seguida, examine a saída de hello. Insira os valores corretos para a máscara de sub-rede hello, o gateway e o prefixo Ipv6, conforme necessário. |

## <a name="error-codes"></a>Códigos do Erro
Os erros estão listados em ordem numérica.

| Número do erro | Texto do erro ou descrição | Ação recomendada do usuário |
|:--- |:--- |:--- |
| 10502 |Foi encontrado um erro ao acessar sua conta de armazenamento. |Aguarde alguns minutos e tente novamente. Se Olá erro persistir, entre em contato com o suporte da Microsoft para as próximas etapas. |
| 40017 |Falha na operação de backup Hello como um volume especificado na política de backup Olá não foi encontrado no dispositivo de saudação. |Repita a operação de backup hello, se hello erro persistir, entre em contato com o Microsoft Support. para as próximas etapas. |
| 40018 |Falha na operação de backup Olá pois nenhum dos volumes de saudação especificados na política de backup Olá foram encontrados no dispositivo de saudação. |Repita a operação de backup hello, se hello erro persistir, entre em contato com o Microsoft Support. para as próximas etapas. |
| 390061 |sistema de saudação está ocupado ou indisponível. |Aguarde alguns minutos e tente novamente. Se Olá erro persistir, entre em contato com o suporte da Microsoft para as próximas etapas. |
| 390143 |Ocorreu um erro com o código de erro 390143. Erro desconhecido. |Se Olá erro persistir, entre em contato com o Microsoft Support para as próximas etapas. |

## <a name="next-steps"></a>Próximas etapas
Se você estiver tooresolve não é possível problema de hello, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) para obter assistência. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
