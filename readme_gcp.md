# fazendo deploy na nuvem 

## utilizando o GCP - google clound platform 

## Passo a passo

### criar conta no google gcp
- Ativar conta

### ativar api
- ativar Compute Engine API

### criar vm
- Criar máquina virtual em "Instâncrias VM"
- nãoe esqueça de libearar http e https 

### usar vm
- clicar no nome da VM "instance...." depois que ela for criada
- clicar em editar e ir até chave ssh 
- adicionar uma
- baixar o putty
- gerar a chave com ele
( mano, mó esquisito isso, provavelmente ssh via terminal é bem mais prático, só que preciso testar então vou por aqui só pela pressa )
- gerar chaves pelo puttygen
- acessar mv pelo putty padrão, dai seleciona a chave privada em browser , usa porta 22, e usa o ip da instancia mv do google. vai em ssh atuh -> credentials -> browser escolha a chave privada .
open
aceita
login é o usuário key comment (é o usuário que acessa a máquina virtual) da chave publica 

### enfiando o docker na mv 
- professor meteu o fodase e nem falou

### colocando o gitlab na bagaça do mv 
- criar um novo projeto no gitlab 
- em configurações -> ci/cd -> runners (executores)
- - pesquisar install gilab runner debian para por ele dentro da mv 
"curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash"
- - na mv entrar em /home/<nome do usuario>
- - - sudo apt update
- - - instala a bagaçça
- - - confirmação :
"The repository is setup! You can now install packages.

- - depois sudo apt install gitlab-runner
- - yes 

### registrar o servidor como runner 
- sudo gitlab-runner register 
- enfia a url da instancia 
- - https://gitlab.com/
- no gitlab crie um executor 
- - escolha linux 
- cole o termo token que ele passa lá no putty que está esperando 
preencha as requisições com cuidado , escolha "shell" no _executer docker_
- teste gitlab-runner start
- em git lab configuração -> ci/cd -> runners ou executores, vai aparecer o projeto lá 
- na mv vc testa cat /etc/passwd para ver se aparece no fum o gitlab runne 

### instale o docker 
- user o guia de install docker on debian 

### dar permissão de docker ao usuário gcp
- sudo usermod -aG docker gcp
- sudo usermod -aG docker gitlab-runner 

### faça login no docker hub 
- via broser internet
- saiba sua senha 

### na mv via puttin
- precisa trocar de usuário
- - sudo su 
- - su gitlab-runner
- precisa de login no docker
- - docker login

### fazer agora com o usuário que criou no nome da public key
- NO MEU caso foi gcp
- então
- exit
- su gcp
- docker login 
- exit 

### clonar o gitlab repositório no seu pc e abrir com vscode
- vai estar zero bala, crie uma pasta app e taca o docker file la dentro 

### saber como chamar a instancia externa (gcp)
- no gitlab vai 
- - configuracao
- - ci/cd 
- -  runner ou executor
no runner que criou e veja a tag que está nele 
se não tiver add uma lá parça
