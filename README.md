# configuracao-servidor-linux-udacity

## IP

A aplicaçao pode ser acessado através do ip 52.205.212.228 com as urls  http://52.205.212.228/ ou http://52.205.212.228/restaurants

## Resumo dos procedimentos realizados para configurar o servidor

### Criação de uma instância Amazon Lightsail

Foi criada uma instância simples e gratuita para configuração do servidor;

### Atualização dos Pacotes de instalação

Todos os pacotes foram instalados logo após a criação da instância;

### Configuração das portas

A porta default de acesso à instância foi alterada de 22 para 2200 através da interface de configuração e aterando o arquivo sshd_config em /etc/ssh/sshd_config

O Uncomplicated Firewall (UFW) foi configurado para permitir somente conexões de entrada para SSH (porta 2200), HTTP (porta 80) e NTP (porta 123).

### Criação do usuário "grader"

Foi criado um novo usuário chamado grader e foi dada a permissão para sudo foi dado a ele;

### Segurança

O comando key-gen foi utilizado para criar um par de chaves para o usuário grader (Até então o acesso era feito com o usuário e senha default da instância).

Foram criados um diretório .ssh e um arquivo authorized_keys com permissão 700 e 644 respectivamente para o novo usuário grader;

O contúdo da chave pública do usuário gradder foi adicionado ao arquivo authorized_keys no servidor. A chave privado foi adicionada ao diretório ssh da máquina local.

O acesso à instância através de password foi bloqueado.

### Time zone

O time zone da instância para America/Sao_Paulo (-02, -0200)

### Apache e WSGI

O Apache foi instalado juntamente como o pacote do WSGI para Python 3.

### Posgres

O Postgres foi instalado na versão 10.

Foi criado um usuário chamado grader com a senha "q1w2e3r4" atribuida a ele.

Foi criado um banco de dados chamado catalog e todos os privilégios relacionados a ele foram dados a grader.

