---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - serviço"
description: "Guias de solução de problemas para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Guia de solução de problemas de serviço
Olá seguem possíveis problemas que podem ocorrer com a execução do Azure Mobile Engagement.

## <a name="service-outages"></a>Interrupções de serviço
### <a name="issue"></a>Problema
* Problemas que aparecem toobe causado por interrupções no serviço do Azure Mobile Engagement.

### <a name="causes"></a>Causas
* Problemas que aparecem toobe causado por interrupções no serviço do Azure Mobile Engagement podem ser causados por vários problemas diferentes:
  * Problemas isolados que originalmente aparecem tooall sistemática do Azure Mobile Engagement
  * Problemas conhecidos causados por interrupções de servidor (nem sempre são mostrados no status do servidor):
  * Agendando atrasos, erros de direcionamento, problemas de atualização do selo, parada estatísticas coletando Push parar de funcionar, da API pararem de funcionar, novos aplicativos ou usuários não pode ser criado, erros DNS e tempo limite Olá da interface do usuário, a API ou aplicativos em um dispositivo.
  * Interrupções de dependência de nuvem [Status do serviço do Azure](http://status.azure.com/)
  * Interrupções de dependência de Serviços de notificação de envio (PNS)
  * Interrupções de loja de aplicativos

1) tootest toosee se problema de saudação sistemático, você pode testar Olá a mesma função de outro

* Aplicativo integrado Azure Mobile Engagement
* Dispositivo de teste
* Versão do SO do dispositivo de teste
* Campanha
* Conta de usuário administrador
* Navegador (IE, Firefox, Chrome, etc.)
* Computador

2) tootest se Olá afeta apenas Olá Olá ou interface do usuário da API:

* Saudação de teste mesma função de ambos os Olá interface de usuário do Azure Mobile Engagement e Olá da API do Azure Mobile Engagement.

3) tootest se o problema de saudação à sua rede de celular:

* Testar enquanto toohello conectado à Internet por meio de WIFI e enquanto estiver conectado por meio de sua rede de celular 3G.
* Confirme se o firewall não está bloqueando qualquer um dos endereços IP do hello Azure Mobile Engagement ou portas.

4) tootest se Olá problema com seu dispositivo:

* Teste se o dispositivo é capaz de tooconnect tooAzure Mobile Engagement com outro aplicativo integrado do Azure Mobile Engagement.
* Verifique se você pode gerar eventos, trabalhos e falhas de seu telefone que pode ser visto no hello interface de usuário do Azure Mobile Engagement. 
* Testar se você pode enviar notificações por push do dispositivo de tooyour de interface de usuário do Azure Mobile Engagement Olá com base em sua ID de dispositivo. 

5) tootest se Olá problema com seu aplicativo:

* Instale e teste seu aplicativo de um emulador em vez de um dispositivo físico:

6) tootest se Olá problema com o sistema operacional atualizado tooend usuário dispositivos, o que requer um tooresolve de atualização do SDK:

* Teste seu aplicativo em dispositivos diferentes com diferentes versões do SO de saudação.
* Confirme que você estiver usando a versão mais recente de saudação do hello SDK.

## <a name="connectivity-and-incorrect-information-issues"></a>Conectividade e problemas de informações incorretas
### <a name="issue"></a>Problema
* Problemas ao efetuar logon em Olá interface de usuário do Azure Mobile Engagement.
* Erros de Conexão com hello API do Azure Mobile Engagement.
* Problemas ao carregar marcas de informações do aplicativo por meio de saudação API do dispositivo.
* Problemas de download de logs ou de dados exportados do Azure Mobile Engagement.
* Informações incorretas mostradas no hello interface de usuário do Azure Mobile Engagement.
* Informações incorretas mostradas nos logs do Azure Mobile Engagement.

### <a name="causes"></a>Causas
* Confirme que sua conta de usuário tem a tarefa de saudação de tooperform permissões suficientes.
* Confirme que esse problema Olá não é isolado tooone ou sua rede local.
* Verifique se esse serviço do Azure Mobile Engagement Olá tem sem interrupções relatadas.
* Confirme se os arquivos de marca de informações do aplicativo seguem todas estas regras:
  * Use Olá apenas o conjunto de caracteres UTF8 (conjunto de caracteres ANSI Olá não tem suporte).
  * Use uma vírgula "," como o caractere separador hello (você pode abrir um serviço toorequest toochange hello. csv separador de caracteres de solicitação de uma vírgula "," caractere tooanother como um ponto e vírgula ";").
  * Usam letras maiúsculas para valores boolianos “verdadeiro” e “falso”.
  * Use um arquivo que é menor do que o tamanho máximo do arquivo de saudação de 35MB.

