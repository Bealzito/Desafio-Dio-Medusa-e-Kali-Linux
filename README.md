# Desafio-Dio-Medusa-e-Kali-Linux
Primeiro foi configurado um virtualbox com kali linux e metaexploit 2 para executar as atividades.  
Após configurado e verificado a conexão utilizando o comando no terminal do Kali ping -c 3 192.168.56.102
Usando o comando nmap -sV -p 21,22,80,445,139 192.168.56.102 foi possivel mapear quais portas estavam abertas no ambiente metaexploit
o alvo da simulação era a porta ftp, de número 21, que estava aberta
Usou os comandos para criação de uma lista de usuários e uma de senhas, sendo eles respectivamente echo -e "user\nmsfadmin\nadmin\nroot" > users.txt e echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
Depois executou-se o comando medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ftp -t 6 para realizar o processo de força bruta, fazendo combinação de usuários e senhas
Outro procedimento foi o ataque de força bruta em formulários de login web, usando a plataforma DVWA e usando de um login e senha errado, acessando o console de desenvolvedor, indo na opção de Network, indo na opção com metodo de POST e acessando Request para entender os parametros utilizados pelo site.
Vale salientar que o DVWA é um site feito para simulações de invasão e já pode se notar alguns aspectos de insegurança no design quando o site indica, por exemplo, que somente o "login falhou" ou somente a "senha falhou".
Para o exercicio, foi utilizado de wordlists, listas com logins e senhas possiveis para fazer o ataque força bruta, existem diversas listas que podem ser resgatadas na internet, inclusive devido a vazamentos de sites.
Também foi abordado o conceito de password spraying, usando o comando enum4linux -a 192.168.56.102 | tee enum4_output.txt, o primeiro comando é para realizar enumeração, enquanto o segundo comando é para gerar um documento de texto com as informações retornadas após executar o comando.
Para password spray, alguns parametros são diferentes, incialmente se utiliza ambos comandos echo -e, tanto para gerar um texto de usuários quanto de senhas, mas o comando de medusa neste cenário é diferente, $ medusa -h 192.168.56.102 -U smb_users.txt -P pass_spray.txt -M smbnt -t 2 -T 50, sendo as principais diferenças no final, tendo alteração do parametro -M smbnt é para ataques via smbnt, -t 2 é para simular 2 threads simultaneas (2 usuários testando senhas) e o -T 50 o número de hosts em paralelo. 
<img width="1920" height="923" alt="image" src="https://github.com/user-attachments/assets/11714d00-e308-4885-891b-d23700785af6" />
Usando  comando smbclient -L //192.168.56.102 -U msfadmin foi possivel executar o login via client do smb, usando usário e senha recuperados no comando anterior.

