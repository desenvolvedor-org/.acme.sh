# AutoSSL
## Install AutoSSL em hospedagem godaddy com renovaçao a cada 3 meses

Essa instalaçao é baseada na instalaçao original do acme
para mais explicaçoes acess https://github.com/acmesh-official/acme.sh

obs: essa instalaçao deve ser feito por alguem que tenha conhecimento de php e ssh

## Instalando o primeiro SSL
#### NO CMD WINDOWS:

1 = abra o cmd em modo administrador

2 = ssh username@888.888.888.88

3 = curl https://get.acme.sh | sh -s email=seuemail@gmail.com

4 = cd .acme.sh
#### NO SITE GODADDY:
5 = crie uma key prod em https://developer.godaddy.com/keys 
#### NO GERENCIADOR DE ARQUIVOS DO CPAINEL:
6 = depois Copia para /.acme.sh/account.conf (GD_Key='xxxxxtpTEP3_xxxxxx9dn3Tdwv8PZxxxxx') e (GD_Secret='xxxxxtmxxxxxZwuWrxxxxx');
#### NO CMD WINDOWS:
7 = export GD_Key='xxxxxtpTEP3_xxxxxx9dn3Tdwv8PZxxxxx'

8 = export GD_Secret='xxxxxtmxxxxxZwuWrxxxxx'


9 = ./acme.sh --server letsencrypt  \
     --issue  -d  seudominio.com -d  *.seudominio.com \
     --dns dns_gd
#### NO GERENCIADOR DE ARQUIVOS DO CPAINEL:
10 = edite o arquivo /.acme.sh/deploy/cpanel_uapi.sh retire o # da linha e coloque seu nome de usuario "export DEPLOY_CPANEL_USER=username"

#### NO CMD WINDOWS:
11 = ./acme.sh --deploy -d seudominio.com -d *.seudominio.com --deploy-hook cpanel_uapi

--------------------certificado instalado com sucesso -----------------------------

## Instale o renovador de Certificados automaticos
#### NO CMD LOGADO NO SSH DO SITE:
1 = cd; cd www

2 = git clone https://github.com/aldejan/AutoSSLnotify.git

#### NO GERENCIADOR DE ARQUIVOS DO CPAINEL:
3 = edite o arquivo www/AutoSSLnotify/notify.php, coloque seu email e o dominio.

#### NO CPAINEL EDITE O CRON:

4 = delete esse comando =  39	0	*	*	*	"/home/v16wlg8p87pp/.acme.sh"/acme.sh --cron --home "/home/v16wlg8p87pp/.acme.sh" > /dev/null

5 = crie esse comando  = 0	0	20	*/2	* cd /home/xxxxxxx/.acme.sh > /dev/n>&1; ./acme.sh --server letsencrypt --force --issue -d seudominio.com -d *.seudominio.com --dns dns_gd > /dev/null 2>&1; ./acme.sh --deploy -d seudominio.com -d *.seudominio.com --deploy-hook cpanel_uapi > /dev/null 2>&1; curl https://www.seudominio.com/AutoSSLnotify/notify.php > /dev/null 2>&1

-------------------AGORA SEU CERTIFICADO SERA RENOVADO A CADA 2 MESES E 20 DIAS-------------------

## Codigos Uteis
#### instalar ssl para unico site ou subdominio:
./acme.sh --server letsencrypt  \
     --issue  -d  livemocha.store \
     -w /home/v16wlg8p87pp/public_html
     
 #### instalar acme por esse repositorio:
 git clone https://github.com/aldejan/AutoSSL.git
 
 cd AutoSSL
 
 ./acme.sh --install -m seuemail@gmail.com
 
 obs: coloque todos os arquivos em permissao 755
 
    

