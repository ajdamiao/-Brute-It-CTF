# -Brute-It-CTF
walkthrough Brute It CTF

1- Primeiramente vou enumerar utilizando o nmap e gobuster
![enumeração](https://imghub.io/i/xonmJ)

2- Com o nmap achei as portas 80(Apache) e 22(OpenSSH) abertas e com o gobuster acheio o diretorio /admin/

3- Acessando a pagina /admin/ encontrei um formulario de login, e ao inspecionar elemento da pagina encontrei a seguinte linha comentada: " Hey john, if you do not remember, the username is admin" 

4- Fazendo o bruteforce com o login admin utilizando o hydra posso conseguir a senha para esse usuario. Como resultado do hydra consegui a senha xavier. usuario: admin senha: xavier

5- Ao fazer login na pagina consegui a primeira flag e uma RSA private key

6- com o bruteforce do john consegui a senha para a hash, agora posso fazer login no SSH utilizando a RSA e o usuario john.

7- Consegui fazer o login, agora dando o comendo ls, listei um arquivo com nome user.txt, dando o comando cat no arquivo consigo a segunda flag (user flag)

8- Agora com o comando sudo -l vou ver quais comandos o usuario john pode usar como sudo, ele pode usar o comando cat entao como sei q preciso da flag do root posso tentar dar o comando sudo cat /root/root.txt para pegar a flag root caso tenha esse arquivo, consegui com sucesso pegar a terceira flag (root flag)

9- Mas tbm posso tentar ler o arquivo /etc/shadow onde contem todos os usuarios e os hash das senhas.

10- Copiando esse arquivo posso utilizar o jhon para pegar a senha do root a senha e football.

11- dando o comando su root posso mudar o usuario e colocar a senha adquirida, consegui acesso ao root, e assim na pasta /root consigo a terceira flag
