# Apuntes sobre Git

## Iniciación
Podemos ver en xeral todos os comandos de git só poñendo `git` na terminal
O primeiro é abrir o directorio no que traballamos e logo o entorno para abrir o VSCode dende a terminal de Conda

```
conda activate name_env
cd .\directorio
code .
```

%% isto realmente xa non fai falla
Agora abrimos a terminal en VSC e abrimos o directorio. En xeral pde ser máis sinxelo traballar dende o prompt de conda
```cd .\directorio```

Podemos ver os arquivos que hai con `ls` coas opcións
```
ls -Attributes 
ls -Directory 
ls -File
ls -Hidden
ls -ReadOnly
ls -System
```
Para incluír o noso repositorio en en git poñemos na terminal 

```
git init
ls -Hidden
```

ten que aparecer un arquivo .git. Agora temos un rexistro de versións, vemos o estado con

```
git status
```

Dinos 3 cousas: en que branch estamos, se se fixeron commits e que cousas están sen actualizar (trackear)

## Xestión arquivos

Para facer un trackeo da área de traballo a un área intermedia entre a de traballo e o repositorio utilizamos
```
git add .\file
```
Se queremos facer un commit para gardalo ben no repositorio (facer unha imaxe freeze)
```
git commit -m "nota explicativa sober as modificacións que fixen"
```
Podemos sacar un log que nos imprima os comentarios das modificacións
```
git log
```
Tamén cando teñamos un ficheiro na área intermedia (i.e., fixemos un `add` pero aínda non un `commit`) podemos comparar os cambios que temos cos cambios no repositorio de git con
```
git diff --staged
```
Isto ábrenos o visor de _less_ que é un pouco raro e non nos deixa facer moitas cousas, temos as seguintes opcións:
* Espazo → avanzar unha páxina.
* b → retroceder unha páxina.
* ↑ / ↓ → mover unha liña.
* /texto → buscar.
* q → saír.







Se quero ver os procesos activos de git, semellante con calquera exe, podo usar
```
tasklist | findstr git
```
para logo  se  teño algún proceso que quedou en erro (o cal xa me pasou dúas veces porque son un inepto podo elimnar o ficheiro de bloqueo)
```
del .git\index.lock
```

Arquivos como os `ipynb_checkpoints` non interesa gardalos