## Configuración de Git en Mac

[Git](https://git-scm.com) es un sistema de control de versiones muy popular. 

[GitHub](https://github.com) es un servicio que te permite cargar, alojar y administrar tu código usando Git con una buena interfaz web.

### Instalar Git

1. Instalar Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Instalar Git
   
```bash
brew install git
```
Abrir una nueva ventana de terminal y comprobar la versión de Git instalada.
```bash
git --version
```

3. Crear una cuenta de [GitHub](https://github.com)

>Para que Git funcione correctamente, necesitamos hacerle saber quiénes somos para que pueda vincular a un usuario local de Git (tú) a GitHub. Al trabajar en un equipo, esto permite a las personas ver lo que has cometido y quién ha cometido cada línea de código.

4. Configuración
   
Los siguientes comandos configurarán Git. ¡Asegúrese de introducir su propia información dentro de las comillas (pero incluya las comillas)!

```bash
git config --global user.name "Axel Santos"
git config --global user.email "axelsan@example.com"
```

Para verificar que las cosas funcionen correctamente, introduzca estos comandos y verifique si la salida coincide con su nombre y dirección de correo electrónico.

```bash
git config --get user.name
git config --get user.email
```

>Ejecuta estos dos comandos para decirle a Git que los ignore. Archivos DS_Store, que se crean automáticamente cuando usas Finder para buscar en una carpeta. . Los archivos de DS_Store son invisibles para el usuario y contienen atributos o metadatos personalizados (como miniaturas) para la carpeta, y si no configuras Git para ignorarlos, es molesto. Los archivos de DS_Store aparecerán en sus confirmaciones. Recuerde copiar y pegar cada uno de estos comandos en su terminal.

```bash
echo .DS_Store >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

### Crear una clave SSH

Una clave SSH es un identificador criptográficamente seguro. Es como una contraseña muy larga que se utiliza para identificar tu máquina. GitHub utiliza claves SSH para permitirle cargar en su repositorio sin tener que escribir su nombre de usuario y contraseña cada vez.

Primero, necesitamos ver si ya tiene instalada una clave SSH del algoritmo Ed25519. Escriba esto en el terminal y compruebe la salida con la siguiente información:

```bash
ls ~/.ssh/id_ed25519.pub
```

Si aparece un mensaje en la consola que contiene el texto "No hay archivo o directorio de este tipo", entonces aún no tiene una clave SSH Ed25519, y tendrá que crear una. Si no ha aparecido dicho mensaje en la salida de la consola, puede continuar a "Vincula tu clave SSH con GitHub".

Para crear una nueva clave SSH, ejecute el siguiente comando dentro de su terminal.

```bash
ssh-keygen -t ed25519
```
Cuando le pida una ubicación para guardar la clave generada, simplemente presione Enter

A continuación, le pedirá una contraseña; introduzca una si lo desea, pero no es obligatoria.

### Vincula tu clave SSH con GitHub

Ahora, necesitas decirle a GitHub cuál es tu clave SSH para que puedas enviar tu código sin escribir una contraseña cada vez.

Primero, navegarás hasta donde GitHub recibe nuestra clave SSH. Inicie sesión en GitHub y haga clic en su foto de perfil en la esquina superior derecha. Luego, haga clic en `Settings` en el menú desplegable.

A continuación, en el lado izquierdo, haga clic en `SSH and GPG keys`. Luego, haga clic en el botón verde en la esquina superior derecha que dice `New SSH` Key. Nombra tu clave algo que sea lo suficientemente descriptivo como para que recuerdes de qué dispositivo proviene esta clave SSH, por ejemplo, `macbook-air`. Deja esta ventana abierta mientras realizas los siguientes pasos.

Ahora necesitas copiar tu clave pública SSH. Para hacer esto, vamos a usar un comando llamado `cat` para leer el archivo en la consola. (Tenga en cuenta que la extensión de archivo `.pub` es importante en este caso).

```bash
cat ~/.ssh/id_ed25519.pub
```

Resalte y copie toda la salida del comando. Si siguió las instrucciones anteriores, la salida probablemente comenzará con `ssh-ed25519` y terminará con `username@hostname`.

Ahora, vuelve a GitHub en la ventana de tu navegador y pega la clave que copiaste en el campo clave. Mantenga el tipo de clave como `Authentication Key` y luego haga clic en `Add SSH key`. ¡Has terminado! ¡Has añadido con éxito tu clave SSH!

### Probando tu clave

Siga las [instrucciones de GitHub para probar su conexión SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection?platform=linux). Asegúrese de que la salida de la huella digital en el terminal coincida con una de las [cuatro huellas dactilares públicas de GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). (¡No olvides omitir el `$` cuando copies y pegues el código!).

Deberías ver esta respuesta en tu terminal: 
>Hi username! You've successfully authenticated, but GitHub does not provide shell access.

Si ves este mensaje, has añadido con éxito tu clave SSH

## Fundamentos

**Git** es como un **botón de guardado** para tus archivos y directorios. Oficialmente, Git es un sistema de control de versiones.

Un guardado en un editor de texto registra todas las palabras de un documento como un solo archivo. Solo se le da un registro del archivo, como `essay.doc`, a menos que haga copias duplicadas (que es difícil recordar hacer y realizar un seguimiento de):

`essay-draft1.doc`, `essay-draft2.doc`, `essay-final.doc`

Sin embargo, un guardado en Git registra las diferencias en los archivos y carpetas Y mantiene un registro ahistórico de cada guardado. Esta característica es un cambio de juego. Como desarrollador individual, Git le permite revisar cómo crece su proyecto y ver o restaurar fácilmente los estados de los archivos del pasado. Una vez conectado a una red, Git le permite enviar su proyecto a **GitHub** u otras alternativas como: Bitbucket, **Beanstalk** o **GitLab** para compartir y colaborar con otros desarrolladores.

Mientras que Git funciona en su máquina local, GitHub es un almacenamiento remoto en la web para todos sus proyectos de codificación. 
