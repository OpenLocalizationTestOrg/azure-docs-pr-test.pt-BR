### <a name="noconnection"></a>prefixos de endereço IP da gateway de rede local toomodify - nenhuma conexão de gateway

Se você não tiver uma conexão de gateway e deseja tooadd ou remover os prefixos de endereço IP, use Olá mesmo comando que você usar o gateway de rede local Olá toocreate, [criar local de rede az gateway](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Você também pode usar esse endereço IP de gateway do comando tooupdate Olá para o dispositivo VPN hello. configurações atuais do toooverwrite Olá, use nome existente de saudação do seu gateway de rede local. Se você usar um nome diferente, você pode criar um novo gateway de rede local, em vez de substituir Olá existente.

Cada vez que fizer uma alteração, toda a lista de prefixos Olá deve ser especificado, Olá não apenas o prefixo que você deseja toochange. Especifique somente prefixos Olá que você deseja tookeep. Neste caso, 10.0.0.0/24 e 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify local de rede gateway prefixos de endereço IP - existente de conexão de gateway

Se você tiver uma conexão de gateway e deseja tooadd ou remove os prefixos de endereço IP, você pode atualizar os prefixos de saudação usando [atualização de gateway local de rede az](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar o endereço IP hello prefixos, gateway VPN Olá toodelete não é necessário.

Cada vez que fizer uma alteração, toda a lista de prefixos Olá deve ser especificado, Olá não apenas o prefixo que você deseja toochange. Neste exemplo, 10.0.0.0/24 e 20.0.0.0/24 já estão presentes. Adicionamos Olá prefixos 30.0.0.0/24 e 40.0.0.0/24 e especificar os 4 de prefixos de saudação ao atualizar.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```