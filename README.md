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

Podemos ver os arquivos que hai no directorio con `ls` coas opcións
```
ls -Attributes 
ls -Directory 
ls -File
ls -Hidden
ls -ReadOnly
ls -System
```
Para incluír o noso repositorio en git poñemos na terminal 

```
git init
ls -Hidden
```

ten que aparecer un arquivo .git, que será o noso novo repositorio; este ademais é posible clonalo `git clone <url>` por se queremos facer unha copia de seguridade ou algo así (creo que o entendín mal, isto é poñer un repositorio de GitHub no noso ordenador local). Agora temos un rexistro de versións, vemos o estado con

```
git status
```

Dinos 3 cousas: en que branch estamos, se se fixeron commits e que cousas están sen actualizar (trackear)

### Sobre VSC
O primeiro, para gardar localmente un arquivo facemos ctrl+s. Na columna esquerda do código temos varias cousa interesantes: en primer lugar temos un explorador dos arquivos, podemos ver toda a árbore de ficheiros no directorio sen necesidad de estar usando `ls` cada 3 segundos; logo abaixo temos un outline e logo unha timeline que no indica o que foi pasando co arquivo que está aberto (tanto a nivel local como liñas de git, sinalando tamén os commits cos comentarios e código interno aforrándonos usar `git log`). Tamén podemos aforrarnos estar usando `git status` cada 5 segundos xa que no explorador aparece un código de colores e iniciais que nos indican varias cousas: es o arquivo foi modificado localmente (gardado) aparecerá no explorador como laranxa e coa letra M (de Modified) á dereita, se pon unha U azulada está _untrucked_ (que non hai ningunha versión gardada no branch). Tamén temos á esquerda de todo varias iconas, a terceira é moi útil para traballar coas pólas porque nos fai unha lista dos arquivos que están sen commitear (sexa cal sexa a fase na que estean) e logo abaixo hai unha representación visual dos branchs e até onde chega cada un, así sabemos tamén o que está na nube tamén.

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
* q → saír. **¡¡CAPTION!!** (para saír en xeral de todos esos entornos _less_)


## Corrixir commits

Podemos corrixir de varias maneiras, modificar o comentario (1), desfacer os últimos commit (2) e finalmente restaurar a versión (3)
(1) `git commit --amend` onde modificamos tal cal o texto que nos aparece e logo para gardar e saír facemos `ESC -> : -> wq` e podemos verificar o cambio imprimindo o log
(2) `git reset HEAD~n` onde _n_ é o número de commits en orde que desfacemos (desfacemos os últimos n commits). O reset ten variacións segundo como queremos que opere que son a soft, mixed and hard que se integran como `... reset -soft...`
(3) `git restore archivo` para que o noso arquivo na área de traballo sexa a versión do último commit gardado, así se anteriormente fixemos un reset podemos restaurar unha versión antiga


## Traballo en pólas

Ao crear o git créasenos o _main_ do noso repositorio, pero o normal sería deixar o _main_ como aquela versión funcional e que non conteña erros e cando queres experimentar e modificar en cantidade o código simplemente creamos outra póla para traballar e facer chapuzadas
* `git branch` amosa a lista de pólas no proxecto
* `git branch -c name` crea unha póla de nome "name"
* `git checkout name` move a área de traballo á póla indicada. Tamén vale `git switch name`
* `git branch -d name` elimina a póla seleccionada en caso de querer desbotala
* `git merge nome` fusiona a póla indicada co main (é importante que esteamos antes no main: `git switch main`), hai varios xeitos de fusionar pólas (véxase https://git-scm.com/cheat-sheet). Hai que aportar comentarios como nos commits. Se se nos esquece poñer o `-m` podemos darlle sen problemas e logo escribir o comentario e facer `ESC -> : -> wq`. Podemos ver unha representación visual das pólas na icona das branchs en VSC.

## Subir cousas a GitHub

Isto é o que se chama facer un push. Non sei como baixarme cousas de GitHub (creo que é o pull) se alguén modifica algo a verdade, pero de momento, o que eu modifico, fagoo como segue: creo un repositorio en GitHub co mesmo nome que estou empregando e logo poñer na terminal as seguintes liñas 
```
git remote add origin https://github.com/sebastian-taboas/particulas.git
git branch -M main
git push -u origin main
```
A segunda liña é importante se non teño unha póla que se chame _main_, de feito ao estar facendo isto a miña póla principal chámase _master_


Se quero ver os procesos activos de git, semellante con calquera exe, podo usar
```
tasklist | findstr git
```
para logo  se  teño algún proceso que quedou en erro (o cal xa me pasou dúas veces porque son un inepto podo elimnar o ficheiro de bloqueo)
```
del .git\index.lock
```

Arquivos como os `ipynb_checkpoints` non interesa gardalos e temos que facer que entren no gitignore. Para facer meter algo nun gitignore facemos
```
echo .ipynb_checkpoints/ >> .gitignore
```
ou sexa, "echo .\directorio\archivo\ Se xa fixen un commit onde se subiron podo facer
`git rm -r --cached .ipynb_checkpoints`