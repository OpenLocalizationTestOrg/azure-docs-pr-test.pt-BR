---
title: aaaRDG e usando o RADIUS do servidor do Azure MFA | Microsoft Docs
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação do Gateway de área de trabalho remota (RD) e servidor Azure multi-Factor Authentication usando RADIUS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Gateway de Área de Trabalho Remota e Servidor de Autenticação Multifator do Azure usando RADIUS
Geralmente, o Gateway de área de trabalho remota (RD) usa usuários de tooauthenticate Olá locais dos serviços de política de rede (NPS). Este artigo descreve como tooroute RADIUS solicita fora do hello Gateway de área de trabalho remota (por meio de Olá NPS local) toohello servidor multi-Factor Authentication. Olá combinação do Azure MFA e o Gateway de área de trabalho remota significa que os usuários podem acessar seus ambientes de trabalho de qualquer lugar ao executar a autenticação forte. 

Como não há suporte para a autenticação do Windows para serviços de terminal Server 2012 R2, use toointegrate RADIUS e de Gateway de área de trabalho remota com o servidor MFA. 

Instale Olá servidor Azure multi-Factor Authentication em um servidor separado, quais proxies Olá RADIUS solicitar novamente toohello NPS Olá servidor de Gateway de área de trabalho remota. Após o NPS validar Olá nome de usuário e senha, ele retorna uma resposta toohello servidor multi-Factor Authentication. Em seguida, Olá servidor MFA executa segundo fator Olá de autenticação e retorna um gateway de toohello do resultado.

## <a name="prerequisites"></a>Pré-requisitos

- Um servidor de MFA do Azure ingressado em um domínio. Se você não tiver um já instalado, siga as etapas de saudação em [guia de Introdução com hello servidor Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
- Um Gateway de Área de Trabalho Remota que autentica com os Serviços de Política de Rede.

## <a name="configure-hello-remote-desktop-gateway"></a>Configurar Olá Gateway de área de trabalho remota
Configure Olá Gateway RD toosend RADIUS autenticação tooan servidor Azure multi-Factor Authentication. 

1. No Gerenciador de Gateway de área de trabalho remota, clique em nome do servidor de saudação e selecione **propriedades**.
2. Vá toohello **repositório RD CAP** guia e selecione **servidor Central que executa o NPS**. 
3. Adicione um ou mais servidores de autenticação de multifator do Azure como servidores RADIUS digitando o nome da saudação ou endereço IP de cada servidor. 
4. Crie um segredo compartilhado para cada servidor.

## <a name="configure-nps"></a>Configurar o NPS
Olá Gateway RD usa NPS toosend Olá RADIUS solicitação tooAzure multi-Factor Authentication. tooconfigure NPS, primeiro você alterar configurações de tempo limite de saudação tooprevent Olá Gateway de área de trabalho remota do tempo limite antes de verificação em duas etapas de saudação foi concluída. Em seguida, você deve atualizar as autenticações de RADIUS do NPS tooreceive do servidor MFA. Use Olá procedimento tooconfigure NPS a seguir:

### <a name="modify-hello-timeout-policy"></a>Modificar a diretiva de tempo limite de saudação

1. No NPS, abra Olá **clientes RADIUS e servidor** menu Olá esquerda da coluna e selecione **grupos de servidores remotos RADIUS**. 
2. Selecione Olá **o grupo de servidor de GATEWAY TS**. 
3. Vá toohello **balanceamento de carga** guia. 
4. Alterar os dois Olá **o número de segundos sem resposta antes que uma solicitação é considerada ignorados** e hello **número de segundos entre as solicitações ao servidor é identificado como indisponível** toobetween 30 e 60 segundos. (Se você encontrar que esse servidor de saudação ainda tempo limite durante a autenticação, você pode volte aqui e aumentar o número de saudação de segundos.)
5. Vá toohello **autenticação/conta** guia e verifique se a portas RADIUS Olá especificado correspondência Olá portas que Olá servidor multi-Factor Authentication está escutando.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Preparar as autenticações tooreceive NPS Olá servidor MFA

1. Clique com botão direito **clientes RADIUS** em clientes RADIUS e servidores em Olá esquerda da coluna e selecione **novo**.
2. Adicione Olá servidor Azure multi-Factor Authentication como um cliente RADIUS. Escolha um nome amigável e especifique um segredo compartilhado.
3. Olá abrir **políticas** menu Olá esquerda da coluna e selecione **diretivas de solicitação de Conexão**. Você deve ver uma política chamada POLÍTICA DE AUTORIZAÇÃO DO GATEWAY de TS que foi criada quando o Gateway de RD foi configurado. Esta política encaminha solicitações RADIUS toohello servidor multi-Factor Authentication.
4. Clique com botão direito em **POLÍTICA DE AUTORIZAÇÃO DE GATEWAY TS** e selecione **Duplicar Política**. 
5. Abrir Olá nova política e ir toohello **condições** guia.
6. Adicione uma condição que corresponda a saudação nome amigável com o nome amigável do hello definido na etapa 2 para o cliente RADIUS do servidor Azure multi-Factor Authentication de saudação do cliente. 
7. Vá toohello **configurações** guia e selecione **autenticação**.
8. Alterar Olá provedor de autenticação muito**autenticar solicitações nesse servidor**. Essa política garante que quando NPS recebe uma solicitação RADIUS de saudação servidor Azure MFA, a autenticação de saudação ocorre localmente, em vez de enviar um RADIUS solicitação back toohello servidor de autenticação multifator do Azure, pode resultar em uma condição de loop. 
9. tooprevent uma condição de loop, certifique-se de que nova política de saudação é ordenada acima a política original Olá no hello **diretivas de solicitação de Conexão** painel.

## <a name="configure-azure-multi-factor-authentication"></a>Configurar a Autenticação Multifator do Azure

Olá servidor Azure multi-Factor Authentication é configurado como um proxy RADIUS entre RD Gateway e NPS.  Ele deve ser instalado em um servidor ingressado no domínio que é separado do servidor de Gateway de área de trabalho remota de saudação. Use Olá Olá do procedimento tooconfigure servidor Azure multi-Factor Authentication a seguir.

1. Abra Olá servidor Azure multi-Factor Authentication e selecione o ícone de autenticação RADIUS hello. 
2. Verificar Olá **habilitar autenticação RADIUS** caixa de seleção.
3. Na guia de clientes hello, certifique-se de portas Olá correspondem ao que está configurado no NPS e selecione **adicionar**.
4. Adicione o endereço IP do servidor de Gateway de área de trabalho remota Olá, nome do aplicativo (opcional) e um segredo compartilhado. Olá compartilhado necessidades secretas toobe Olá mesmo Olá servidor Azure multi-Factor Authentication e o Gateway de área de trabalho remota.
3. Vá toohello **destino** guia e selecione Olá **servidores RADIUS** botão de opção.
4. Selecione **adicionar** e insira o endereço IP hello, segredo compartilhado e portas do servidor NPS de saudação. A menos que usando um NPS central, Olá cliente RADIUS e o destino RADIUS são Olá mesmo. segredo compartilhado Olá deve corresponder a configuração Olá na Olá seção de cliente RADIUS do servidor NPS de saudação.

![Autenticação Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Próximas etapas

- Integrar o Azure MFA e [aplicativos web do IIS](multi-factor-authentication-get-started-server-iis.md)

- Obtenha respostas no hello [perguntas frequentes sobre o Azure multi-Factor Authentication](multi-factor-authentication-faq.md)
