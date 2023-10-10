# AutoSSL
## Install AutoSSL em hospedagem godaddy com renovaçao a cada 3 meses

Essa instalaçao é baseada na instalaçao original do acme
para mais explicaçoes acess https://github.com/acmesh-official/acme.sh

obs: essa instalaçao deve ser feito por alguem que tenha conhecimento de php e ssh
use um bloco de notas para pegar os codigos e editalos antes de mandar para cmd.

Essa primeira forma é a nativa, mais caso nao funcionar verifique a segunda forma em [https://github.com/desenvolvedor-org/AutoSSL/wiki](https://github.com/desenvolvedor-org/.acme.sh/wiki)

## Instalando o primeiro SSL
#### NO CMD WINDOWS:

1 = abra o cmd em modo administrador

2 = ``ssh username@888.888.888.88``

3 = ``curl https://get.acme.sh | sh -s email=seuemail@gmail.com``
Alternativa: ``git clone https://github.com/Livemochas/.acme.sh.git``

4 = ``cd .acme.sh``

5 = ``./acme.sh --set-default-ca  --server letsencrypt``

#### NO SITE GODADDY:
6 = crie uma key prod em https://developer.godaddy.com/keys 

#### NO GERENCIADOR DE ARQUIVOS DO CPAINEL:
7 = depois Copia para /.acme.sh/account.conf (SAVED_GD_Key='xxxxxtpTEP3_xxxxxx9dn3Tdwv8PZxxxxx') e (SAVED_GD_Secret='xxxxxtmxxxxxZwuWrxxxxx');

#### NO CMD WINDOWS:

8 = ``export GD_Key='xxxxxtpTEP3_xxxxxx9dn3Tdwv8PZxxxxx'``

9 = ``export GD_Secret='xxxxxtmxxxxxZwuWrxxxxx'``


10 = ``./acme.sh --server letsencrypt --issue -d seudominio.com -d *.seudominio.com --dns dns_gd``

#### NO GERENCIADOR DE ARQUIVOS DO CPAINEL:
11 = edite o arquivo /.acme.sh/deploy/cpanel_uapi.sh retire o # da linha e coloque seu nome de usuario "export DEPLOY_CPANEL_USER=username"

12 = edite agora o arquivo /.acme.sh/notify/mail.sh retire o # da linha e coloque seu email de envio e os emails que voce quer receber as notificaçoes quando for renovado o certificado, e altere as permissoes do arquivo para 755.
MAIL_FROM="sistemas@seudominio.com"
MAIL_TO="usearname@hotmail.com,username@gmail.com" 

#### NO CMD WINDOWS:

13 = ``./acme.sh --set-notify  --notify-hook mail --notify-level 2 --notify-mode 0``

14 = ``./acme.sh --deploy -d seudominio.com -d *.seudominio.com --deploy-hook cpanel_uapi``

--------------------certificado instalado com sucesso -----------------------------

## Verifique se o renovador de Certificados automaticos esta ativo.
#### NO CPAINEL EDITE O CRON:

1 = verifique se existe um comando similar a esse =  

``39	0	*	*	*	"/home/xxxxxxxx/.acme.sh"/acme.sh --cron --home "/home/xxxxxxxx/.acme.sh" > /dev/null``

obs: esse comando é criado automanticamente e vai renovar seu certificado a cada 2 meses.

## Atualize manualmente o certificado.
#### NO CMD WINDOWS:

1 = abra o cmd em modo administrador

2 = ``ssh username@888.888.888.88``

3 = ``cd .acme.sh``

4 = ``./acme.sh --deploy -d seudominio.com -d *.seudominio.com --deploy-hook cpanel_uapi``
