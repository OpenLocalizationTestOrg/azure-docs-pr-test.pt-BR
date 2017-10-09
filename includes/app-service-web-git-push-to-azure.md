## <a name="push-tooazure-from-git"></a>TooAzure de envio por push do Git

Adicione um repositório Git local do Azure tooyour remoto.

```bash
git remote add azure <URI from previous step>
```

Enviar seu aplicativo por push toohello toodeploy remoto do Azure. Você será solicitado para senha Olá criado anteriormente ao criar usuário de implantação de saudação. Certifique-se de que você insira a senha Olá criada na [configurar um usuário de implantação](#configure-a-deployment-user), Olá a senha não use toolog em toohello portal do Azure.

```bash
git push azure master
```

Olá precede o comando exibe informações semelhantes toohello exemplo a seguir:
