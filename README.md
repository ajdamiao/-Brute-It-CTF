# -Brute-It-CTF
walkthrough Brute It CTF

1- Primeiramente vou enumerar utilizando o nmap e gobuster

2- Com o nmap achei as portas 80(Apache) e 22(OpenSSH) abertas e com o gobuster acheio o diretorio /admin/
![Enumaracao](https://user-images.githubusercontent.com/52061729/101178822-345c7b80-3628-11eb-8037-d8aaa1116e3f.png)

3- Acessando a pagina /admin/ encontrei um formulario de login, e ao inspecionar elemento da pagina encontrei a seguinte linha comentada: " Hey john, if you do not remember, the username is admin" 
![Login Page](https://user-images.githubusercontent.com/52061729/101178889-4b02d280-3628-11eb-8d13-517519f8261b.png)

4- Fazendo o bruteforce com o login admin utilizando o hydra posso conseguir a senha para esse usuario. Como resultado do hydra consegui a senha xavier. usuario: admin senha: xavier
![Hydra](https://user-images.githubusercontent.com/52061729/101178972-640b8380-3628-11eb-8972-9de2ee2147a1.png)

5- Ao fazer login na pagina consegui a primeira flag e uma RSA private key
![Admin](https://user-images.githubusercontent.com/52061729/101179005-6ff74580-3628-11eb-8c0d-219c82eea9e6.png)

![RSA](https://user-images.githubusercontent.com/52061729/101179105-97e6a900-3628-11eb-8e54-07f684e6204e.png)

6- utilizando o ssh2john e johntheripper consegui a senha para a chave RSA, agora posso fazer login no SSH utilizando a RSA e o usuario john.
![RSA.hash](https://user-images.githubusercontent.com/52061729/101179271-c82e4780-3628-11eb-9f3b-71b4ccd3df9c.png)

7- Consegui fazer o login, agora dando o comendo ls, listei um arquivo com nome user.txt, dando o comando cat no arquivo consigo a segunda flag (user flag)
![SSH john](https://user-images.githubusercontent.com/52061729/101179368-e005cb80-3628-11eb-8b0a-1eaabd3dfcd3.png)

8- Agora com o comando sudo -l vou ver quais comandos o usuario john pode usar como sudo, ele pode usar o comando cat entao como sei q preciso da flag do root posso tentar dar o comando sudo cat /root/root.txt para pegar a flag root caso tenha esse arquivo, consegui com sucesso pegar a terceira flag (root flag)
![sudo -l](https://user-images.githubusercontent.com/52061729/101179398-e8f69d00-3628-11eb-9af1-d170b99ab33e.png)

9- Mas tbm posso tentar ler o arquivo /etc/shadow onde contem todos os usuarios e os hash das senhas.
![etc/shadow](https://user-images.githubusercontent.com/52061729/101179509-117e9700-3629-11eb-9a51-9c802053fa0c.png)

10- Copiando esse arquivo posso utilizar o jhon para pegar a senha do root a senha e football.

11- dando o comando su root posso mudar o usuario e colocar a senha adquirida, consegui acesso ao root, e assim na pasta /root consigo a terceira flag
![Screenshot_12](https://user-images.githubusercontent.com/52061729/101179577-2d823880-3629-11eb-8672-c30b83423428.png)
