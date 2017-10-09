---
title: aaaAzure Mobile Engagement Troubleshooting Guide - envio/alcance
description: "Solucionando problemas de notificação e interação do usuário no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Guia de solução para problemas de Push e Reach
Olá seguem possíveis problemas que podem ser encontrados em como o Azure Mobile Engagement envia informações tooyour os usuários.

## <a name="push-failures"></a>Falhas de push
### <a name="issue"></a>Problema
* Os pushes não funcionam (no aplicativo, fora do aplicativo ou ambos).

### <a name="causes"></a>Causas
* Uma falha de envio por push muitas vezes é uma indicação de que Azure Mobile Engagement, alcance ou outro recurso avançado do Azure Mobile Engagement não está corretamente integrado ou que uma atualização é necessária Olá SDK toofix um problema conhecido com uma nova plataforma de sistema operacional ou o dispositivo.
* Teste apenas um envio por push no aplicativo e apenas um toodetermine de envio por push do aplicativo se algo é um problema no aplicativo ou do aplicativo.
* Teste de saudação da interface do usuário e Olá API como uma solução de problemas toosee de etapa quais informações de erro adicionais estão disponíveis dois locais.
* Fora do aplicativo envios por Push não funcionarão a menos que o Azure Mobile Engagement e alcance estão integrados Olá SDK.
* Os pushes não funcionarão se os certificados não forem válidos ou estiverem usando PROD versus DEV corretamente (somente iOS). (**Observação:** "fora do aplicativo" notificações por push podem não ser entregue tooiOS, se você tiver dois desenvolvimento hello (desenvolvimento) e versões de produção (produção) do seu aplicativo instalado em Olá mesmo dispositivo desde Olá token de segurança associado com o seu certificado pode ser invalidado pela Apple. tooresolve esse problema, desinstale Olá desenvolvimento e produção de versões do seu aplicativo e reinstale somente Olá uma versão em seu dispositivo.)
* Fora do aplicativo por push contagens são tratadas diferentemente em diferentes plataformas (iOS mostra menos informações que Android se envios por push nativo estão desabilitados em um dispositivo, Olá API pode fornecer mais informações de saudação da interface do usuário nas estatísticas de envio por push).
* Os pushes Fora do Aplicativo podem ser bloqueados pelos clientes ao nível do SO (iOS e Android).
* Envios por push fora do aplicativo serão mostrados como desativado no hello interface de usuário do Azure Mobile Engagement se não estiver integrados corretamente, mas pode falhar em modo silencioso da saudação API.
* No aplicativo envios por Push não funcionarão a menos que o Azure Mobile Engagement e alcance estão integrados Olá SDK.
* Envios por push GCM e ADM não funcionarão a menos que o Azure Mobile Engagement e servidor específicos Olá estão integrados Olá SDK (somente Android).
* No aplicativo e fora do aplicativo envios por push devem ser separadamente testada toodetermine se for um problema de envio por Push ou de alcance.
* No aplicativo envios requerem que o aplicativo hello toobe abrir recebido.
* No aplicativo envios por push geralmente são filtrado por uma marca de informações do aplicativo de aceitação ou recusa de toobe de instalação.
* Se você usar uma categoria personalizada em notificações do alcance toodisplay no aplicativo, é necessário toofollow Olá correto ciclo de vida de notificação de saudação, caso contrário, não pode ser limpa a notificação de saudação ao usuário Olá descartá-lo.
* Se você iniciar uma campanha com nenhuma data de término e um dispositivo recebe a saudação na notificação do aplicativo, mas não exibi-lo ainda, Olá usuário ainda receberá Olá Olá de notificação próxima vez que fizerem logon no aplicativo hello, mesmo se você encerrar a campanha Olá manualmente.
* Para problemas com hello API por Push, confirme que você realmente deseja toouse Olá API por Push em vez da saudação API de alcance (desde Olá API de alcance é usado com mais frequência) e que não é confuso hello "carga" e os parâmetros "notificação".
* Teste sua campanha de push com dois um dispositivo conectado por Wi-Fi e 3G tooeliminate Olá rede conexão como uma possível fonte de problemas.

## <a name="push-testing"></a>Teste do Push
### <a name="issue"></a>Problema
* Envios por push podem ser enviados tooa dispositivo específico com base em uma ID de dispositivo.

### <a name="causes"></a>Causas
* Dispositivos de teste são diferentes para cada plataforma, mas fazendo com que um evento em seu aplicativo em um dispositivo de teste e observando a ID do dispositivo no portal de saudação devem funcionar toofind a ID do dispositivo para todas as plataformas.
* Os dispositivos de teste funcionam de forma diferente com IDFA versus IDFV (iOS apenas).

## <a name="push-customization"></a>Personalização do Push
### <a name="issue"></a>Problema
* O item de conteúdo do push avançado não funcionará (notificação, toque, vibração, imagem etc.).
* Links de envios por Push não funcionam (fora do aplicativo, no aplicativo, site tooa, tooa local no aplicativo).
* Mostrar estatísticas de envio que um envio por push não foi enviado tooas muitas pessoas conforme esperado (muitos ou insuficiente).
* Push duplicado e recebido duas vezes.
* Não é possível registrar o dispositivo de teste para os Pushes do Azure Mobile Engagement (com seu próprio aplicativo PROD ou DEV).

### <a name="causes"></a>Causas
* tooa de toolink local específico no aplicativo requer "categorias" (somente Android).
* Profundo de esquemas de vinculação local alternativo do tooredirect usuários tooan depois de clicar em uma notificação por push necessário toobe criado no e gerenciados pelo seu aplicativo e hello SO do dispositivo não pelo Mobile Engagement diretamente. (**Observação:** fora do aplicativo notificações não é possível vincular diretamente tooin locais de aplicativo com o iOS como podem Android.)
* Servidores de imagem externa precisam toobe capaz de toouse HTTP "GET" e "HEAD" para o panorama envia toowork (somente Android).
* No seu código, você pode desabilitar o agente do Azure Mobile Engagement hello quando o teclado de saudação é aberto e têm seu código reativar o agente do Azure Mobile Engagement hello quando teclado Olá for fechado para que hello teclado não afeta a aparência de saudação do seu notificação (somente iOS).
* Alguns itens não funcionam nas simulações de teste, mas somente nas campanhas reais (notificação, toque, vibração, imagem etc.).
* Nenhum lado servidor dados são registrados quando você usar o botão de saudação muito "testar" envia. Os dados só são registrados para as campanhas de push reais.
* toohelp isolar o problema, solucionar problemas com: teste, simular e uma campanha real, desde que cada um deles funcionam de forma ligeiramente diferente.
* Olá tempo que seu "no aplicativo" e campanhas de "sempre" são toorun agendada pode afetar a números de entrega desde uma campanha serão entregues somente toousers que estão "aplicativo" durante a execução de campanha hello (e os usuários que têm suas configurações de dispositivo definem tooreceive notificações "fora do aplicativo").
* diferenças de saudação entre como o identificador do Android e iOS notificações do aplicativo torna difícil toodirectly comparam as estatísticas de envio entre a versão Android e iOS saudação do seu aplicativo. O Android fornece mais informações de notificação ao nível do SO do que o iOS. Android informa quando uma notificação nativa é recebida, clicada ou excluída no Centro de notificação hello, mas iOS não relatar essas informações, a menos que a notificação de saudação é clicada. 
* Olá principal motivo que números "enviados" são diferentes de diferentes de números "entregues" para alcançar campanhas é que "no aplicativo" e "fora do aplicativo" notificações são contadas diferentemente. "No aplicativo" notificações são manipuladas pelo Mobile Engagement, mas "fora do aplicativo" notificações são manipuladas pelo Centro de notificação de saudação em Olá SO do dispositivo.

## <a name="push-targeting"></a>Direcionamento do push
### <a name="issue"></a>Problema
* O direcionamento incorporado não funciona conforme o esperado.
* O direcionamento da Marca de Informações do Aplicativo não funciona conforme o esperado.
* O direcionamento da Localização Geográfica não funciona conforme o esperado.
* As opções de idioma não funcionam conforme o esperado.

### <a name="causes"></a>Causas
* Certifique-se de que você carregou marcas de informações do aplicativo por meio de saudação do Azure Mobile Engagement UI ou API.
* Limitação Olá velocidade ou push cota push no nível de aplicativo hello ou limitação público Olá no nível da campanha de saudação pode impedir que uma pessoa receber um envio por push específico, mesmo se eles atendem aos seus outros critérios de destino. 
* Definir um "Idioma" é diferente de direcionar com base no país ou na localidade, que também é diferente de direcionar com base na Localização geográfica em um telefone local ou GPS.
* mensagem de saudação em hello "idioma padrão" é enviada cliente tooany que não tenha o seu dispositivo definido tooone de idiomas alternativos hello, que você especificar.

## <a name="push-scheduling"></a>Agendamento do push
### <a name="issue"></a>Problema
* O agendamento do push não funciona conforme o esperado (enviado muito cedo ou atrasado).

### <a name="causes"></a>Causas
* Fusos horários pode problemas com o agendamento, especialmente ao usar o fuso horário Olá dos usuários finais.
* Os recursos avançados do push podem atrasar os pushes.
* Direcionamento com base no telefone configurações (em vez de marcas de informações de aplicativo) podem atrasar envia desde que o Azure Mobile Engagement pode ter dados toorequest Olá telefone em tempo real antes de enviar um envio por push.
* Campanhas criadas sem uma data de término armazenam Olá push localmente no dispositivo hello e mostrá-lo Olá próxima vez aplicativo hello for aberto, mesmo que a campanha Olá é encerrada manualmente.
* Iniciar mais de uma campanha em Olá a mesmo tempo pode levar uma tooscan de tempo mais longo sua base de usuários (tente tooonly iniciar uma campanha por vez com um máximo de quatro, apenas usuários ativos tooyour de destino também, para que os usuários não tenham toobe verificado).
* Se você usar a opção de "Ignorar público, push será enviado toousers via API de hello" Olá, na seção de "Da campanha" hello de uma campanha de alcance, campanha de saudação não enviará automaticamente, você precisará toosend-los manualmente por meio de saudação API de alcance.
* Se você usar uma categoria personalizada em notificações do alcance toodisplay no aplicativo, é necessário toofollow Olá correto ciclo de vida de uma notificação, caso contrário, não pode ser limpa a notificação de saudação ao usuário Olá descartá-lo.

