# configuracao-servidor-linux-udacity

## IP

A aplicação pode ser acessado através do ip 52.205.212.228 com as urls  http://52.205.212.228/ ou http://52.205.212.228/restaurants

## Resumo dos procedimentos realizados para configurar o servidor

### Criação de uma instância Amazon Lightsail

Foi criada uma instância simples e gratuita para configuração do servidor;

### Atualização dos Pacotes de instalação

Todos os pacotes foram instalados logo após a criação da instância;

### Configuração das portas

A porta default de acesso à instância foi alterada de 22 para 2200 através da interface de configuração e aterando o arquivo sshd_config em /etc/ssh/sshd_config. Caso tente fazer o acesso pela porta 22 ocorrerá um timeout.

O Uncomplicated Firewall (UFW) foi configurado para permitir somente conexões de entrada para SSH (porta 2200), HTTP (porta 80) e NTP (porta 123).

O Uncomplicated Firewall (UFW) foi configurado para negar a acesso pela porta 22.

### Criação do usuário "grader"

Foi criado um novo usuário chamado grader e foi dada a permissão para sudo foi dado a ele;

### Segurança

O comando key-gen foi utilizado para criar um par de chaves para o usuário grader (Até então o acesso era feito com o usuário e senha default da instância).

Foram criados um diretório .ssh e um arquivo authorized_keys com permissão 700 e 644 respectivamente para o novo usuário grader;

O contúdo da chave pública do usuário gradder foi adicionado ao arquivo authorized_keys no servidor. A chave privado foi adicionada ao diretório ssh da máquina local.

O acesso à instância através de password foi bloqueado no arquivo sshd_confgi como trecho específico ficando "PasswordAuthentication no".

### Time zone

O time zone da instância para America/Sao_Paulo (-02, -0200)

### Apache e WSGI

O Apache foi instalado juntamente como o pacote do WSGI para Python 3.

### Postgres

O Postgres foi instalado na versão 10.

Foi criado um usuário chamado grader com a senha "q1w2e3r4" atribuida a ele.

Foi criado um banco de dados chamado catalog e todos os privilégios relacionados a ele foram dados a grader.

Pelas minhas pesquisas o Postgres já vem desabilitado para acesso remoto com o administrador tendo que fazer o processo de habilitar o mesmo caso necessário.

### Configurando a aplicação "catalog"

O projeto foi clonado no diretório /var/www/html;

No mesmo diretório foi criado um arquivo de configuração chamado catalog.wsgi

Um arquivo requirements.txt foi executado com sudo pip3 install -r para instalar as bibliotecas necessárias para execução do prejeto. 

O arquivo /etc/apache2/sites-enabled/000-default.conf foi editado configurando o virtual host da aplicação.

O arquivo database_setup.py foi exectuado para criar as tabelas da aplicação no banco catalog e lot_of_menus.py foi executado para popular o banco com alguns valores pré-definidos.

### Acesso remoto como root

A possibilidade de acesso remoto do usuário root foi impedido alterando o arquivo sshd_config com o treche específico ficando "PermitRootLogin no";

### Referências para pesquisa:

https://stackoverflow.com/  
https://www.vivaolinux.com.br/  
https://modwsgi.readthedocs.io/en/develop/  
http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/  
https://github.com/kongling893/Linux-Server-Configuration-UDACITY  
https://my.esecuredata.com/index.php?/knowledgebase/article/7/allow-or-deny-a-port-ufw-ubuntu  
https://debian-administration.org/article/69/Some_upgrades_show_packages_being_kept_back  
