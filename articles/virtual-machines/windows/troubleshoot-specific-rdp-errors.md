---
title: "mensagens de erro RDP aaaSpecific para máquinas virtuais do Azure | Microsoft Docs"
description: "Entender as mensagens de erro específicas que podem ser exibidas durante a tentativa de usam a máquina de virtual do Windows de tooa de conexão de área de trabalho remota no Azure"
keywords: "Erro de área de trabalho remoto, erro de conexão de área de trabalho remota, não é possível conectar tooVM, solução de problemas da área de trabalho remota"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Solução de problemas específico tooa de mensagens de erro RDP VM do Windows no Azure
Você pode receber uma mensagem de erro específica ao usar a área de trabalho remota conexão tooa máquina virtual do Windows (VM) no Azure. Este artigo detalha algumas das Olá encontradas, junto com tooresolve de etapas de solução de problemas de mensagens de erro mais comuns-los. Se você estiver tendo problemas para se conectar tooyour VM usando o RDP não mas não encontrar uma mensagem de erro específica, consulte Olá [guia para a área de trabalho remota de solução de problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obter informações sobre mensagens de erro específicas, consulte o seguinte hello:

* [sessão remota Olá foi desconectada porque não há nenhum tooprovide de servidores de licenças de área de trabalho remota disponível uma licença](#rdplicense).
* [Área de trabalho remota não é possível encontrar hello "nome do computador"](#rdpname).
* [Ocorreu um erro de autenticação. Olá autoridade de segurança Local não pode ser contatada](#rdpauth).
* [Erro de Segurança do Windows: suas credenciais não funcionaram](#wincred).
* [Este computador não é possível conectar o computador remoto toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>sessão remota Olá foi desconectada porque não há nenhum tooprovide de servidores de licenças de área de trabalho remota disponível uma licença.
Causa: Olá 120 dias licenciamento período de cortesia para a função de servidor de área de trabalho remota de saudação expirou e você precisar tooinstall licenças.

Como alternativa, salve uma cópia local do arquivo RDP de saudação do portal hello e execute este comando em um tooconnect de prompt de comando do PowerShell. Essa etapa desabilita o licenciamento apenas para esta conexão:

        mstsc <File name>.RDP /admin

Se mais de dois simultâneas área de trabalho remota conexões toohello VM, na verdade, não é necessário, você pode usar a função de servidor de área de trabalho remota Olá tooremove do Gerenciador do servidor.

Para obter mais informações, consulte Olá postagem de blog [VM do Azure falha "Sem servidores licenças de área de trabalho remota disponíveis"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Área de trabalho remota não é possível localizar o computador hello "name".
Causa: o cliente de área de trabalho remota de saudação em seu computador não pode resolver o nome de saudação do computador Olá nas configurações de saudação do arquivo RDP de saudação.

Soluções possíveis:

* Se você estiver na intranet da organização, certifique-se de que o computador tem acesso toohello proxy server e pode enviar tooit do tráfego HTTPS.
* Se você estiver usando um arquivo RDP armazenado localmente, tente usar Olá um que é gerado pelo portal de saudação. Essa etapa garante que você tem nome DNS correto de saudação para a máquina virtual de hello, ou serviço de nuvem hello e porta do ponto de extremidade de saudação do hello VM. Aqui está um arquivo RDP de exemplo gerado pelo portal hello:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

parte do endereço Olá deste arquivo RDP tem:

* Olá totalmente qualificado de nome de domínio do serviço de nuvem Olá contém Olá VM ("tailspin-azdatatier.cloudapp.net" neste exemplo).
* porta TCP de externa Hello, do ponto de extremidade Olá para o tráfego de área de trabalho remota (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Ocorreu um erro de autenticação. Olá autoridade de segurança Local não pode ser contatado.
Causa: VM de destino Olá não pode localizar autoridade de segurança Olá parte de nome de usuário de saudação de suas credenciais.

Quando seu nome de usuário está na forma de saudação *SecurityAuthority*\\*UserName* (exemplo: corp/User1), Olá *SecurityAuthority* parte é o hello VM nome do computador (para a autoridade de segurança local Olá) ou um nome de domínio do Active Directory.

Soluções possíveis:

* Se houver Olá conta local toohello VM, certifique-se de que nome VM Olá foi digitado corretamente.
* Se a conta de saudação estiver em um domínio do Active Directory, verifique a ortografia de Olá Olá do nome de domínio.
* Se for uma conta de domínio do Active Directory e Olá domínio nome foi digitado corretamente, verifique se um controlador de domínio está disponível nesse domínio. É um problema comum em redes virtuais do Azure que contêm controladores de domínio que um controlador de domínio não esteja disponível porque ele ainda não foi iniciado. Como alternativa, você pode usar uma conta de administrador local em vez de uma conta de domínio.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Erro de Segurança do Windows: suas credenciais não funcionaram.
Causa: o destino Olá VM não é possível validar seu nome de conta e senha.

Um computador baseado no Windows pode validar as credenciais de saudação de uma conta local ou uma conta de domínio.

* Para contas locais, use Olá *ComputerName*\\*UserName* sintaxe (exemplo: SQL1\Admin4798).
* Para contas de domínio, use Olá *DomainName*\\*UserName* sintaxe (exemplo: CONTOSO\peterodman).

Se você tiver promovido a controlador de domínio tooa VM em uma nova floresta do Active Directory, a conta de administrador local Olá que você entrou é convertida tooan equivalente conta com hello mesma senha em Olá nova floresta e domínio. conta local Olá é excluída.

Por exemplo, se você está conectado com a conta local de saudação DC1\DCAdmin e, em seguida, promovida Olá VM como um controlador de domínio em uma nova floresta de domínio corp.contoso.com de saudação, Olá DC1\DCAdmin conta local é excluída e uma nova conta de domínio (CORP\DCAdmin ) é criado com hello mesma senha.

Verifique se o que nome dessa conta Olá é um nome que máquina virtual de saudação pode verificar como uma conta válida, e essa senha hello está correta.

Se precisar toochange Olá senha da conta de administrador local hello, consulte [como tooreset uma senha ou hello área de trabalho remota de serviço para máquinas virtuais do Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Este computador não pode conectar o computador remoto toohello.
Causa: conta Olá que usou tooconnect não tem direitos de área de trabalho remota.

Cada computador do Windows tem um área de trabalho remota usuários grupo local, que contém contas de saudação e grupos que podem entrar remotamente. Membros do grupo de administradores locais Olá também têm acesso, mesmo que essas contas não são listadas no grupo de usuários local da área de trabalho remota de saudação. Para computadores que ingressaram no domínio, o grupo de administradores locais Olá também contém Olá administradores de domínio Olá domínio.

Certifique-se de que a conta de saudação com que estiver usando tooconnect tem direitos de área de trabalho remota. Como alternativa, use um domínio ou tooconnect de conta de administrador local na área de trabalho remota. tooadd Olá o grupo de usuários de área de trabalho remota local toohello conta desejada, use o snap-in Console de gerenciamento Microsoft hello (**ferramentas do sistema > usuários e grupos locais > grupos > Remote Desktop Users**).

## <a name="next-steps"></a>Próximas etapas
Se nenhum desses erros ocorreram e tem um problema desconhecido com a conexão usando o RDP, consulte Olá [guia para a área de trabalho remota de solução de problemas](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Para solucionar problemas de etapas ao acessar aplicativos em execução em uma máquina virtual, consulte [aplicativo de tooan acesso de solução de problemas em execução em uma VM do Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Se você estiver tendo problemas para usar o Secure Shell (SSH) tooconnect tooa VM do Linux no Azure, consulte [solucionar problemas de SSH conexões tooa VM do Linux no Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

