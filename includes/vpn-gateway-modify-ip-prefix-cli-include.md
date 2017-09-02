### <a name="noconnection"></a>Para modificar prefixos de endereço IP de gateway de rede local - sem conexão de gateway

Se você não tiver uma conexão de gateway e deseja adicionar ou remover os prefixos de endereço IP, você use o mesmo comando que você usa para criar o gateway de rede local, [az network local-gateway create](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Você também pode usar esse comando para atualizar o endereço IP do gateway para o dispositivo VPN. Para sobrescrever as configurações atuais, use o nome existente do seu gateway de rede local. Se você usar um nome diferente, um novo gateway de rede local será criado, em vez de substituir o existente.

Sempre que você fizer uma alteração, toda a lista de prefixos deverá ser especificada, não apenas os prefixos que você deseja alterar. Especifique apenas os prefixos que você deseja manter. Neste caso, 10.0.0.0/24 e 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>Para modificar prefixos de endereço IP de gateway de rede local - conexão de gateway existente

Se você tiver uma conexão de gateway e deseja adicionar ou remover os prefixos de endereço IP, você pode atualizar os prefixos usando [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar os prefixos de endereço IP, você não precisa excluir o gateway de VPN.

Sempre que você fizer uma alteração, toda a lista de prefixos deverá ser especificada, não apenas os prefixos que você deseja alterar. Neste exemplo, 10.0.0.0/24 e 20.0.0.0/24 já estão presentes. Podemos adicionar os prefixos 30.0.0.0/24 e 40.0.0.0/24 e especificar todos os 4 prefixos durante a atualização.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```