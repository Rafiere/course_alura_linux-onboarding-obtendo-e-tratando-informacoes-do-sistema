# AULA 01

Um script nada mais é do que uma **sequência de comandos**.

Nesse curso, faremos um script de backup, em que, ao informarmos um determinado diretório, esse script obterá todas as pastas desse diretório e copiará para outro diretório.

## VARIÁVEIS DO SISTEMA

O comando `env` exibe todas as variáveis que estão atribuídas no sistema.

O comando `echo $nomedavariavel` exibe o valor de uma variável.

## SHEBANG

A primeira linha de um script bash deve possuir o `#!/bin/bash`, o operador `#!` é chamado de `shebang`, e ele define para o script identificar qual o shell que será utilizado.

Por padrão, utilizaremos o `bash`.

Abaixo, teremos o código do script.

```shell
#!/bin/bash

echo "digite o diretório de backup:"

read diretorio_bkp

cp -rv $diretorio_bkp ~/backup

echo ""
echo "O backup foi concluído!"
```

O nome do script deverá ser `backup.sh`. O `.sh` é a extensão utilizada para arquivos que são feitos na linguagem **_Shell Script_**.

Após criarmos esse arquivo com o script, temos que fornecer a **permissão de execução** desse script para o dono do arquivo, dessa forma, temos que utilizar o comando `chmod u+x backup.sh`, assim, estamos fornecendo essa permissão.

O comando `./backup.sh` executará esse arquivo de script.

Dentro do diretório `/usr/bin` temos os binários dos comandos que os usuários podem executar no sistema.

## VARIÁVEL $PATH

A variável de ambiente `$PATH` contém os diretórios em que, ao digitarmos um comando no terminal, os binários desse comando serão buscados.

Após adicionarmos o comando script `backup.sh` no diretório `/bin`, podemos apenas utilizar o comando `backup.sh` de qualquer lugar do terminal para que esse script seja executado.

# AULA 02

## OBTENDO INFORMAÇÕES DA REDE

Antigamente, o comando `ifconfig` era necessário para verificarmos informações da rede, porém, atualmente, temos o comando `ip`.

O comando `ip addr` exibe informações sobre o IP do usuário.

Nesse comando, o `enp0s3`, por exemplo, é o nome da interface de rede. No `inet`, temos o IP que está associado à essa máquina.

O comando `hostname -I` exibe o IP do usuário.

O diretório `/etc/resolv.conf` possui os servidores de nome, ou seja, os servidores DNS que a máquina está utilizando. Para alterarmos o servidor DNS, temos que alterar o IP do servidor DNS na string `nameserver endereco-do-servidor-dns` para o servidor DNS desejado.

O comando `ping ip` serve para realizarmos um ping no IP informado.

## OBTENDO INFORMAÇÕES DO COMPUTADOR

O comando `sudo lshw` listará informações do hardware da máquina.

O diretório `/proc` contém várias informações sobre o hardware do computador.

O comando `cat /proc/meminfo` possui informações sobre a memória do computador que está sendo utilizado.

O comando `free` exibe informações da memória. Ele utiliza o arquivo `/proc/meminfo`.

O comando `cat /proc/cpuinfo` informa os dados sobre a CPU do servidor.

## DISPOSITIVOS DE BLOCOS (DISCOS)

As informações dos dispositivos estão no diretório `/dev`.

Os dispositivos de bloco vão aparecer no sistema com as letras `sd`, ou seja, `sda` para o primeiro disco, `sdb` para o segundo disco e etc.

A sigla `sda1` está se referindo à primeira partição, representada pelo `1`, do disco `a`.

O comando `df -h` exibe os discos do usuário.

O `hda1` exibe os discos do tipo `IDE`, que, atualmente, estão em desuso, pois os discos `SATA` estão sendo mais utilizados.

# AULA 03

## PRINCIPAIS ARQUIVOS DE LOG DO SISTEMA

O comando `dmesg` exibe as mensagens de buffer do Kernel. Se utilizarmos o comando `dmesg | grep sda` veremos todos os logs relacionados aos discos que foram enviadas no Kernel.

O arquivo `/var/log/syslog` exibe os logs que foram registrados das execuções do sistema.

O Arquivo `/var/log/auth.log` possui logs sobre a autenticação do sistema. As autenticações que foram bem ou mal sucedidas serão inseridas aqui.

O comando `tail -f nome-do-arquivo` deixa o arquivo aberto, e, a cada entrada do arquivo, o arquivo será alterado em tempo real.

Existe uma **rotação de logs** dentro do Linux, assim, por exemplo, quando os logs passam uma determinada quantidade de dias, é criado um outro arquivo de log e eles vão sendo armazenados, por isso que temos, por exemplo, o `auth.log.1`, o `auth.log.2` e etc.

O arquivo que configura essa rotação de logs é o `/etc/logrotate.conf`.

# AULA 04

## LISTANDO PROCESSOS COM O PS E TOP

Para cada atividade executada no Linux, um processo será gerado.

O comando `ps -e` exibe uma foto resumida da situação dos processos que estão ativos no computador.

O comando `ps -ef` exibe informações detalhadas sobre os processos.

O `PID` é o ID do processo, e o `PPID` é o ID do processo-pai de um determinado processo.

O comando `ps aux` exibe o consumo de CPU, de memória e outras informações sobre os processos que estão ativos no sistema.

Enquanto o `ps` tira uma foto do sistema, o `top` exibe as informações dinâmicas dos processos. Por padrão, o comando `top` exibe os processos pelo consumo de memória.

Dentro do comando `top`, se apertarmos o `P`, os processos serão ordenados por consumo de CPU. Se apertarmos `m`, os processos serão ordenados pelo consumo de memória. O `n` ordenará os processos por PID, ou seja, quanto maior o PID, mais tardiamente o processo foi inicializado no sistema, e se apertarmos o `t`, os processos serão ordenados pelo tempo em que eles estão em execução.

## INSTALANDO SERVIDOR WEB

O comando `sudo apt install apache2` instalará o pacote do servidor Apache.

O Apache é um dos servidores web mais utilizados.

O comando `sudo service apache2 status` exibe o status do Apache e se ele está executando.

Após o serviço do apache estar sendo executado, basta utilizarmos o comando `ip addr` e inserirmos esse IP no browser, e, dessa forma, sermos redirecionados para a página inicial do Apache.

Dentro do diretório `/proc`, temos vários diretórios para os processos que foram inicializados no Linux.

## GERENCIANDO PROCESSOS COM O KILL

Existem vários sinais para trabalharmos com os processos. O comando `kill -l` lista todos os sinais existentes no sistema.

O `SIGKILL`, que é o sinal de número `9`, mata o processo. Isso pode gerar algumas consequências. Se enviarmos esse comando para um banco de dados em produção, isso poderá causar erros de inconsistências de dados.

O `SIGTERM`, que é o sinal de número `15`, indica para as aplicações que estão prontas para suportar esse sinal que o sistema deseja fechar essa aplicação, assim, a aplicação encerra as sessões, realiza salvamentos e etc.

O comando `kill -9 6229` encerrará o processo cujo o PID é `6229`. O comando `kill` passa um sinal para os processos.

Se utilizarmos apenas o comando `kill PID`, o sinal `15`, ou seja, o `SIGTERM` será enviado para o processo, assim, ele não será interrompido de forma abrupta.

Quando matamos um processo-pai, todos os processos filhos são encerrados.

O comando `pstree` exibe os processos no formato de árvore.

# AULA 05

## ESCALANDO PRIVILÉGIOS COM O SUDO

Não é recomendado utilizarmos o sistema como um usuário privilegiado, ou seja, não devemos ficar logados com usuários administrativos.

Quando queremos utilizar um usuário administrativo, utilizamos o comando `sudo nome-do-comando` para executarmos um determinado comando com privilégios administrativos.

O comando `sudo` funciona apenas para usuários especiais, e não para todos os usuários.

O arquivo `/etc/sudoers` possui informações sobre os grupos que podem executar o comando `sudo`.

O comando `groups` exibe os grupos que o usuário pertence.

O arquivo `/etc/group` possui os grupos e os usuários existentes em cada grupo do sistema.

O comando `su` permite que troquemos de usuário. O comando `sudo su` serve para entrarmos como `root`. A `home` do usuário `root` é o `/root`. A `home` dos usuários normais é `/home/nome-do-usuario`.

## DIFERENÇAS ENTRE O ROOT E OS DEMAIS USUÁRIOS

O comando `exit` serve para deslogarmos da conta atual.

O comando `passwd` serve para alterarmos a senha do usuário atual.

Quando estamos como `root`, conseguimos utilizar o comando `passwd nome-do-usuario`, assim, trocaremos a senha do usuário sem precisarmos da senha antiga.

O arquivo `/etc/shadow` armazena o hash da senha dos usuários, o algoritmo de hash que é utilizado e etc.

## USUÁRIOS DO SISTEMA

O comando `sudo service apache2 start` serve para iniciarmos o serviço do Apache.

Se tentarmos trocar para um usuário do sistema, um erro será gerado, pois o shell desse usuário é o `/usr/sbin/nologin`, ou seja, ele não possui um shell definido.
