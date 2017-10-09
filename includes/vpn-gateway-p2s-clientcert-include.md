Cada computador cliente que se conecta tooa VNet usando ponto a Site deve ter um certificado de cliente instalado. certificado de saudação do cliente é gerado a partir do certificado de raiz de saudação e instalado em cada computador cliente. Se um certificado de cliente válido não está instalado e o cliente Olá tenta tooconnect toohello VNet, a autenticação falhará.

Você pode gerar um certificado exclusivo para cada cliente, ou você pode usar o hello mesmo certificado para vários clientes. certificados de cliente exclusivos Olá vantagem toogenerating é Olá capacidade toorevoke um único certificado. Caso contrário, se vários clientes usando Olá mesmo certificado de cliente e é necessário toorevoke-lo, você toogenerate e instalar novos certificados para todos os clientes que usam esse certificado tooauthenticate de hello.

Você pode gerar os certificados de cliente usando Olá métodos a seguir:

- **Certificado corporativo:**

  - Se você estiver usando uma solução de certificado corporativo, gerar um certificado de cliente com o formato de valor de nome comum Olá 'name@yourdomain.com', em vez de formato de 'domínio localizados' hello.
  - Verifique se o certificado de cliente Olá é baseado no modelo de certificado do hello 'User' que tem 'Autenticação de cliente' como o primeiro item na lista de uso de saudação de Olá, em vez de inteligente de Logon de cartão, etc. Você pode verificar o certificado de saudação clicando duas vezes o certificado de cliente hello e exibindo **detalhes > uso avançado de chave**.

- **Certificado raiz autoassinado:** é importante que você siga etapas Olá Olá P2S certificado artigos abaixo. Caso contrário, os certificados de cliente Olá que criar não sejam compatíveis com conexões de P2S e os clientes recebem um erro durante a tentativa de tooconnect. etapas de saudação em qualquer um dos artigos a seguir de saudação geram um certificado de cliente compatível: 

  * [Instruções do Windows 10 PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): essas instruções exigem certificados de toogenerate do Windows 10 e o PowerShell. certificados Olá gerados podem ser instalados em qualquer cliente P2S com suporte.
  * [Instruções de MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): Use MakeCert se você não tiver acesso tooa Windows 10 computador toouse toogenerate certificados. MakeCert preterido, mas você ainda pode usar o MakeCert toogenerate certificados. certificados Olá gerados podem ser instalados em qualquer cliente P2S com suporte.

  Quando você gerar um certificado de cliente de um certificado raiz autoassinado usando Olá anterior instruções, ele tem instalado automaticamente no hello computador que você usou toogenerate-lo. Se você quiser tooinstall um certificado de cliente em outro computador cliente, você precisa tooexport-lo como um. pfx, juntamente com a cadeia de certificado inteiro hello. Isso cria um arquivo. pfx que contém informações de certificado de raiz de saudação que é necessárias para autenticar Olá toosuccessfully de cliente. Para etapas tooexport um certificado, consulte [certificados - exportar um certificado de cliente](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
