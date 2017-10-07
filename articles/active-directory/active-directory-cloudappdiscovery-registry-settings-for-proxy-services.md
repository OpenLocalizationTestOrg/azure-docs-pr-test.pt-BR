---
title: "Configurações de registro de descoberta do aplicativo para os serviços de Proxy de aaaCloud | Microsoft Docs"
description: "Olá objetivo deste tópico é tooprovide com hello etapas que você precisar de porta de Olá necessário de tooset de tooperform em computadores Olá executando Olá Cloud App Discovery agent."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Configurações de Registro do Cloud App Discovery para serviços de proxy
Por padrão, o agente do Cloud App Discovery Olá é toouse configurado somente Olá portas 80 ou 443. Se você estiver planejando instalar o Cloud App Discovery em um ambiente com um servidor proxy que está usando uma porta personalizada (nem 80 nem 443), você precisa tooconfigure toouse seus agentes essa porta. configuração de saudação baseia-se em uma chave do registro.

Olá objetivo deste tópico é tooprovide com hello etapas que você precisar de porta de Olá necessário de tooset de tooperform em computadores Olá executando Olá Cloud App Discovery agent.

**porta de saudação toomodify usada pelo computador Olá executando o agente do Cloud App Discovery hello, execute Olá etapas a seguir:**

1. Inicie o editor do registro hello. <br> ![Executar](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Navegue tooor criar hello chave do registro a seguir: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. Crie um novo valor de **cadeia de caracteres múltipla** chamado **Portas**. ![Novo](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Olá tooopen **Editar cadeia de caracteres múltipla** caixa de diálogo, clique duas vezes no valor de portas de saudação.
5. No texto de dados de valor hello, digite hello valores a seguir e adicione todas as portas personalizadas que são usadas pela sua organização: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Editar Cadeia de Caracteres Múltipla](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Clique em **Okey** tooclose Olá **Editar cadeia de caracteres múltipla** caixa de diálogo.

**Recursos adicionais**

* [Como descobrir aplicativos na nuvem não aprovados, usados em minha organização](active-directory-cloudappdiscovery-whatis.md) 

