## <a name="create-a-ruby-application"></a>Criar um aplicativo Ruby
Para obter instruções, confira [Criar um aplicativo Ruby no Azure (a página pode estar em inglês)](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu tooUse barramento de serviço do aplicativo
toouse barramento de serviço, baixe e use o pacote do Azure Ruby hello, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use o pacote de saudação do RubyGems tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Usando seu editor de texto favorito, adicione Olá toohello superior de saudação Ruby a seguir na qual você pretende toouse armazenamento de arquivo:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Configurar uma conexão do Barramento de Serviço
Tooset valores de saudação do namespace, nome da saudação de código a seguir de saudação do uso chave, chave, o signatário e host:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Definir Olá namespace toohello valor criado em vez de URL inteira hello. Por exemplo, use **"yourexamplenamespace"**, não "yourexamplenamespace.servicebus.windows.net".
