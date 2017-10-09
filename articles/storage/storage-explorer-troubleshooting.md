---
title: "Guia de solução de problemas de Gerenciador de armazenamento aaaAzure | Microsoft Docs"
description: "Visão geral do recurso de depuração de dois de saudação do Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Guia de solução de problemas do Gerenciador de Armazenamento do Azure

## <a name="introduction"></a>Introdução

Gerenciador de armazenamento do Microsoft Azure (visualização) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Windows e Linux e macOS. Olá aplicativo pode se conectar a contas toStorage hospedadas no Azure, Sovereign nuvens e pilha do Azure.

Este guia resume as soluções de problemas comuns encontrados no Gerenciador de Armazenamento.

## <a name="sign-in-issues"></a>Problemas de entrada

Somente contas do AAD (Azure Active Directory) têm suporte. Se você usar uma conta do AD FS, espera-se que a assinatura no tooStorage que Explorer não funcionará. Antes de continuar, tente reiniciar o aplicativo e veja se os problemas de saudação podem ser corrigidos.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Erro: Certificado autoassinado na cadeia confiável

Há várias razões por que você pode encontrar esse erro, e dois motivos de hello mais comuns são as seguintes:

1. Olá aplicativo está conectado por meio de um "proxy transparente", que significa que um servidor (como o servidor da sua empresa) é interceptar o tráfego HTTPS, descriptografá-los e, em seguida, criptografar usando um certificado autoassinado.

2. Você está executando um aplicativo, como software antivírus, que está injetando um certificado SSL autoassinado em mensagens de saudação do HTTPS que você receber.

Quando o Gerenciador de armazenamento encontra um dos problemas hello, pode não saber se a mensagem de saudação recebida do HTTPS foi violada. Se você tiver uma cópia do certificado autoassinado hello, você pode deixar o Gerenciador de armazenamento deve confiar nele. Se você não tiver certeza de que está injetando certificado hello, siga estas etapas toofind-lo:

1. Instalar o Open SSL

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualquer uma das versões de luz Olá deve ser suficiente)

    - Mac e Linux: deve estar incluído com o sistema operacional

2. Executar Open SSL

    - Windows: Abra o diretório de instalação de saudação, clique em **/bin/**e, em seguida, clique duas vezes em **openssl.exe**.
    - Mac e Linux: execute **openssl** de um terminal.

3. Execute s_client -showcerts -connect microsoft.com:443

4. Procurar certificados autoassinados. Se você não tiver certeza de que são autoassinado, procure em qualquer lugar assunto hello ("s") e emissor ("i") são Olá mesmo.

5. Quando localizar todos os certificados autoassinados, para cada um, copie e cole-tudo a partir e incluindo **---iniciar certificado---** muito**---concluir certificado---** tooa novo arquivo de. cer.

6. Abra o Gerenciador de armazenamento, clique em **editar** > **certificados SSL** > **importar certificados**e, em seguida, use Olá arquivo seletor toofind, selecione, e abra hello. cer que você criou.

Se você não encontrar todos os certificados autoassinados usando Olá acima etapas, entre em contato conosco por meio da ferramenta de comentários Olá para obter mais ajuda.

### <a name="unable-tooretrieve-subscriptions"></a>Não é possível tooretrieve assinaturas

Se você não é possível tooretrieve suas assinaturas depois que você entre com êxito, siga essas etapas tootroubleshoot esse problema:

- Verifique se sua conta tem acesso toohello assinaturas ao entrar em Olá portal do Azure.

- Certifique-se de que você entrou usando o ambiente correto de saudação (do Azure, do Azure na China, Alemanha do Azure, Azure US Government ou personalizado do Azure/ambiente pilha).

- Se você estiver atrás de um proxy, certifique-se de que você tenha configurado proxy de Gerenciador de armazenamento Olá corretamente.

- Tente remover e lendo a conta de saudação.

- Tente excluir Olá seguintes arquivos do diretório raiz (ou seja, C:\Users\ContosoUser) e, em seguida, adicionar novamente conta hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Console de ferramentas de desenvolvedor inspecionar hello (pressionando F12) quando você está tentando entrar para as mensagens de erro:

![ferramentas de desenvolvedor](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Página de autenticação não é possível toosee Olá

Se você página de autenticação Olá toosee não é possível, siga essas etapas tootroubleshoot esse problema:

- Dependendo da velocidade da saudação de sua conexão, ele pode levar algum tempo para tooload de página de entrada hello, aguarde pelo menos um minuto antes de fechar a caixa de diálogo de autenticação de saudação.

- Se você estiver atrás de um proxy, certifique-se de que você tenha configurado proxy de Gerenciador de armazenamento Olá corretamente.

- Exibir o console do desenvolvedor hello, pressionando a tecla F12 de saudação. Assista a respostas de saudação do console do desenvolvedor hello e ver se você pode encontrar qualquer dica de por que a autenticação não está funcionando.

### <a name="cannot-remove-account"></a>Não é possível remover a conta

Se você não é possível tooremove uma conta, ou se Olá reautenticar link não faz nada, siga essas etapas tootroubleshoot esse problema:

- Tente excluir Olá seguintes arquivos do diretório raiz e, em seguida, lendo conta hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Se você quiser tooremove SAS anexado recursos de armazenamento, exclua Olá seguintes arquivos:

    - Pasta %AppData%/StorageExplorer para Windows

    - /Usuários/<seu_nome>/Library/Applicaiton SUpport/StorageExplorer para Mac

    - ~/.config/StorageExplorer para Linux

> [!NOTE]
>  Você terá tooreenter todas as suas credenciais se você excluir esses arquivos.

## <a name="proxy-issues"></a>Problemas de proxy

Primeiro, certifique-se de que Olá segue as informações inseridas estão corretas:

- Olá URL do proxy e a porta número

- Nome de usuário e senha, se exigido pelo proxy Olá

### <a name="common-solutions"></a>Soluções comuns

Se você ainda estiver tendo problemas, siga estas etapas tootroubleshoot-los:

- Se você puder se conectar toohello Internet sem usar o proxy, verifique se o Gerenciador de armazenamento funciona sem as configurações de proxy habilitadas. Se esse for o caso de Olá, pode haver um problema com as configurações de proxy. Trabalhar com seus problemas de saudação do proxy administrador tooidentify.

- Verifique se outros aplicativos usando o servidor de proxy Olá funcionam conforme o esperado.

- Verifique se que você pode conectar o portal do Microsoft Azure toohello usando seu navegador da web

- Verifique se que você pode receber respostas de seus pontos de extremidade de serviço. Insira uma das suas URLs de ponto de extremidade em seu navegador. Se você puder se conectar, deverá receber um InvalidQueryParameterValue ou resposta XML semelhante.

- Se outra pessoa também estiver usando o Gerenciador de Armazenamento com o servidor proxy, verifique se eles podem se conectar. Se eles possam se conectar, você pode ter toocontact seu administrador do servidor proxy.

### <a name="tools-for-diagnosing-issues"></a>Ferramentas para diagnosticar problemas

Se você tem ferramentas de rede, como o Fiddler para Windows, você pode ser capaz de toodiagnose problemas de saudação da seguinte maneira:

- Se você tiver toowork por meio do proxy, você pode ter tooconfigure seu tooconnect ferramenta rede por meio do proxy de saudação.

- Verifique o número da porta Olá usada pela ferramenta de sua rede.

- Digite a URL de host local de saudação e Olá número da porta da ferramenta de rede como configurações de proxy no Gerenciador de armazenamento. Se isso for feito corretamente, a sua rede ferramenta inicia o log de solicitações de rede feitas pelos pontos de extremidade toomanagement e o serviço do Gerenciador de armazenamento. Por exemplo, digite https://cawablobgrs.blob.core.windows.net/ para seu ponto de extremidade de blob em um navegador e você receberá uma resposta semelhante Olá seguinte, o que sugere Olá recurso existir, embora você não pode acessá-lo.

![exemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Entre em contato com o administrador do servidor proxy

Se as configurações de proxy estão corretas, você poderá ter toocontact seu administrador do servidor proxy, e

- Verifique se o proxy não bloqueia o tráfego tooAzure gerenciamento ou o recurso de pontos de extremidade.

- Verifique se o protocolo de autenticação de saudação usado pelo servidor proxy. No momento, o Gerenciador de Armazenamento não dá suporte a proxies NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Mensagem de erro "Não é possível tooRetrieve filhos"

Se você estiver conectado tooAzure através de um proxy, verificar se as configurações de proxy estão corretas. Se você foi concedido acesso tooa recursos proprietário de saudação da saudação assinatura ou conta, verifique se você leu ou lista de permissões para esse recurso.

### <a name="issues-with-sas-url"></a>Problemas com a URL SAS
Se você estiver se conectando tooa serviço usando uma URL SAS e apresentando este erro:

- Verifique se Olá URL contém as permissões necessárias Olá tooread ou lista de recursos.

- Verifique se esse Olá que URL não expirou.

- Se Olá URL SAS é baseado em uma política de acesso, verifique se a política de acesso Olá não foi revogada.

## <a name="next-steps"></a>Próximas etapas

Se nenhuma das soluções de saudação funcionar para você, enviar seu problema por meio da ferramenta de comentários do hello com seu email e como muitos detalhes sobre o problema Olá incluídos como você podem, para que possamos contatá-lo para corrigir o problema de saudação.

toodo, clique **ajuda** menu e clique **enviar comentários**.

![Comentários](./media/storage-explorer-troubleshooting/4022503_en_1.png)
