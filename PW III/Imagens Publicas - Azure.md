# Criando Imagens Públicas na Azure

O Microsoft Azure fornece uma plataforma robusta para armazenar e gerenciar seus dados na nuvem. 

Este tutorial mostrará como criar um Azure Storage Account, criar um contêiner de blob para armazenamento e, em seguida, fazer upload de imagens para esse contêiner. 

## Criando um Storage Account (Conta de Armazenamento)

Acesse o portal da azure com sua conta de estudante

![Alt text](image.png)

Depois, pesquise na barra de recursos por Storage Accounts ou Contas de Armazenamento, dependendo do idioma configurado em sua conta.

![Alt text](assets/image-4.png)

Ao navegar à tela de Contas de armazenamento, crie um novo clicando na opção create (ou criar) no canto superior esquerdo

![Alt text](assets/image-3.png)

Você então sera redirecionado à página de criação de um Storage Account

![Alt text](assets/image-5.png)

Na opção Grupos de Armazenamento você pode criar um novo caso ainda não tenha criado nenhum grupo anteriormente, ou pode reutilizar um criado previamente.

Para criar um novo basta clicar na opção "Criar Novo" e preencher com o nome de seu projeto

![Alt text](assets/image-6.png)

Na opção **Detalhes da instância** você deve criar um nome de armazenamento único, que será utilizado na URL de acesso à sua imagem.

![Alt text](assets/image-7.png)

Agora, navegue para o menu "Avançado", para configurarmos a segurança de nossas imagens.

![Alt text](assets/image-17.png)

Depois, na opção **Segurança**, marque a opção **Permitir a habilitação do acesso anônimo em contêineres individuais*.

![Alt text](assets/image-18.png)

Depois disso clique em **Examinar** no rodapé à esquerda

![Alt text](assets/image-8.png)

Por fim, quando disponível, clique em **Criar** também no rodapé à esquerda.

![Alt text](assets/image-19.png)

Você será redirecionado para uma página de implantação, aguarde a conclusão e clique em "Ir para o recurso"

![Alt text](assets/image-20.png)

Pronto! Ao seguir esse processo você criou a sua Conta de Armazenamento e deve ver uma tela como a tela a seguir:

![Alt text](assets/image-21.png)

## Configurando acesso público à Conta de Armazenamento

Precisamos configurar o acesso anônimo para nossas imagens, para isso, acesse a opção de configurações no menu lateral à esquerda:

![Alt text](assets/image-22.png)

Depois, caso esteja deselecionado, selecione a opção "Permitir acesso anônimo ao Blob"

*Antes*

![Alt text](assets/image-23.png)

*Depois*

![Alt text](assets/image-24.png)

Por fim, clique em salvar no menu superior

![Alt text](assets/image-25.png)

## Criando um Blob Container

No contexto de um Azure Storage Account, um Blob Container (Contêiner de Blob) é um recipiente lógico usado para organizar e armazenar objetos binários, conhecidos como "blobs". 

Esses blobs podem ser arquivos binários, como imagens, vídeos, documentos, backups, ou qualquer outro tipo de dados não estruturados que você deseja armazenar na nuvem.

*Em resumo, podemos entender um container na Conta de Armazenamento como a pasta onde de fato nossos arquivos estarão hospedados*.

Para criar um container, pesquise no menu lateral por Container e acesse sua opção.

![Alt text](assets/image-26.png)

Ao ser redirecionado à tela de Container, clique na opção de adicionar Container

![Alt text](assets/image-27.png)

No menu lateral que abrir, escolha um nome para seu container, esse nome pode ser o nome do seu projeto mesmo, e selecione o nível de acesso **Blob** e clique em criar

![Alt text](assets/image-28.png)

Quando seu container for criado, você deverá ver a tela a seguir

![Alt text](assets/image-29.png)

## Subindo uma imagem via Azure

Acesse o container criado no passo anterior

![Alt text](assets/image-30.png)

Na tela seguinte clique na opção **Caregar**

![Alt text](assets/image-31.png)

No menu lateral, selecione a imagem desejada e clique em carregar.

![Alt text](assets/image-32.png)

A imagem carregada deve apeser na listagem do container

![Alt text](assets/image-33.png)

**Pronto**, sua imagem está criada na nuvem e pronta para acessar de qualquer lugar.

Para pegar sua URL, clique na imagem e no menu que abrir você podera ver e copiar a URL criada

![Alt text](assets/image-34.png)

Ao copiar a URL e acessar no navegador, você poderá ver a sua imagem

![Alt text](assets/image-35.png)