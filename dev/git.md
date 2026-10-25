# GIT

## Externi odkazy

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)  
[Best practice](https://www.git-tower.com/learn/git/ebook/en/command-line/appendix/best-practices)  
[Tutorial on workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/centralized-workflow)  

## užitečné nástroje

[pre-commit](https://pre-commit.com) ... automatické akce v případě volání git hooku, jako třeba git commit. Např automaticky zformátuje a zvaliduje kód  
conventional commits ... prefix konvence commitů pro lepší rozpoznání účelu a pro automatické generování changelogu  
sme  
[auth-changelog](https://github.com/cookpete/auto-changelog) ... automatické generování changelogů  
[článek](https://medium.com/opensight-ch/git-semantic-versioning-and-conventional-commits-564aece418a0) o použití sematického verzování, conventional commits, release note, change logu atd  
[Submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) ... možnost mít v git repozitáři namountované i jiné repozitáře v podadresářích, když máme závislosti na jiné repa  

## git promenne

`git config --global user.name "John Doe"`  
`git config --global user.email johndoe@example.com`  
`git config --list` ... seznam promennyh  
`git config --list --system` ... zobrazi systemove promenne  
`git config --list --global` ... zobrazi globalni promenne  
`git config --list --show-origin` ... zobrazi všechny proměnné a kde jsou definovány  
`git config --global alias.co checkout` ... aliasy  
`git config --global credential.helper cache` ... cachovane kredence  
/etc/gitconfig ... system config  
~/.gitconfig, ~/.config/git/config ... global config  
.git/config ... local config  
`git help` ... help  
`git help remote` ... help k remote  

## Vytvoreni repozitare, prace s repozitari

git init ... vytvoreni lokalniho repozitare v aktualnim adresari  
git clone git@github.rtp.raleigh.ibm.com:tomas.lipensky-cz/bi-dwh_tools.git ... vytvori adresar bi_dwh_tools s klonem repozitare z URL  
git remote -v ... vypise repozitare a jejich adresy v danem git adresari  
git remote ... ukaze aktualni vzdaleny repozitar  
git remote add repo2 URL ... prida novy vzdaleny repozitar (git server)  
git fetch repo2 ... ziskani vsech zmen ve vsech vetvich z git serveru repo2, co nejsou v lokalnim repu, neprepise lokalni soubory  
git pull vetev1 ... fetch z git serveru a aplikovani zmen (merge) na vetev vetev1  
git pull ... fetch a merge  
git push origin master ... publikuje zmeny vetve master na git server origin  
git push origin test:master ... publikuje lokalni vetev test do vzdalene master  
git push ... publikuje zmeny vsech vetvi na aktualni git server  
git remote show repo2 ... ukaze stav na servery repo2  
git remote rename origin repo2 ... prejmenuje git server origin na repo2  

### Prace s kodem, schvalovani zmen, historie

`git status` ... aktualni vetev a zmeny v ni  
`git status -s` ... aktualni zmeny - 1 soubor = 1 radek  
`git add service_scanner.sh *.txt` ... pridani souboru do stage - kontrola GITem, po commitu se to ulozi k dane verzi projektu  
`git blame -L 5,10 helm/values.yaml` ... ukaze autory jednotlivych radku  
`git commit -m "komentar k commitnuti"` ... potvrzeni kodu k odeslani u vsech souboru pridanych pomoci add  
`git commit --amend` ... oprava posledniho commitu  
`git commit --fixup 1e30877` ... commitne zmeny jako opravu commitu 1e30877  
`git reset HEAD service_scanner.sh` ... odebere soubor service_scanner z commitu  
`git reset --hard origin/dev` ... prepise na tvrdo lokalni zmeny ?  
`git checkout -- service_scanner.sh` ... vrati zmeny z service_scanner.sh, ktere jsme provedli v souboru  
[git log](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) ... seznam historie commitu - check sum, popis, datum, autor  
`git log --pretty=oneline` ... jednoradkovy, pouze check sum a popis  
`git log -p` ... ukaze historii i se zmenama  
`git log --stat` ... ukaze jen statistiky zmen  
`git log --oneline -5 --author lipensky --before "Fri Mar 26 2009"` ... filtr pro log  
`git show` ... ukaze posledni zmeny  
`git diff` ... porovna zmeneny soubor oproti puvodnimu (z git lokalnih repozitare)  
.gitignore ... ignore list pro stage a commit  
`git rm a.txt` ... odebere z repozitare a.txt  
`git mv b.txt a.txt` ... prejmenuje v repu b.txt na a.txt  

`git reflog` ... seznam zmen  
`git revert` ... vrati zmeny  
`git reset` ... pozor, muze byt nebezpecne, ztrata zmen  
`git rebase -i --autosquash 7dbe2a9` ... rebase - slouci fixupy (opravy), otevre v rebase interaktivnim modu  
`git merge origin master` ... udela pull commitu z masteru a jejich merge do aktualni vetve  
`git rebase -i HEAD~3` ... rebase poslednich 3 commitu  
`git shortlogs` ... vylistuje comity podle autoru  
`git gc` ... garbage collection  

### Tagy

Vice info: [https://git-scm.com/book/en/v1/Git-Basics-Tagging](https://git-scm.com/book/en/v1/Git-Basics-Tagging)

`git tag -a 1.0.1 -m "applied hotfix 1"` ... prida tag k posledni zmene (commitu)  
`git tag -a 1.0.0 -m "initial version" 20721acbb115cc33848dfcc21` ... otaguje commit, jehoz check sum, nebo jeho cast je v parametru  
`git show 1.0.1` ... ukaze zmeny pro dany tag  
`git tag` ... seznam tagu  
`git tag pracovni` ... prida lehky tag - bez komentaru, k posledimu commitu  
`git tag -l "prac*"` ... vylistuje vsechny tagy, co zacinaji na prac  
`git push REMOTE TAG` ... odesle zmeny do repozitare REMOTE s tagem TAG, jinak se tagy neprenasi  
`git push REMOTE --tags` ... odesle zmeny do repozitare, prenese i tagy  
`git notes add -m "Zkontrolovano 2019/05/12"` ... pridani note  

### Vetve / branches

Vice o vetvich: [https://git-scm.com/book/en/v1/Git-Branching-Basic-Branching-and-Merging](https://git-scm.com/book/en/v1/Git-Branching-Basic-Branching-and-Merging)

git checkout master ... prepne HEAD - ukazatel na aktualni vetev na "master" a prehodi vsechny soubory na aktualni soubory z vetver master  
git checkout -b hotfix1 ... vytvori z aktualni vetve novou vetev hotfix1 a prepne se do ni  
git commit -a -d "oprava hotfix1" ... add (-a = add na vsechny soubory, co se zmenily) a commit (schvaleni zmen)  
git checkout master ... prepne zpet do puvodni vetve  
git branch -d hotfix1 ... smaze vetev hotfix1  
git branch ... seznam vetvi, ukaze aktualni  
git checkout -b hotfix1 origin/hotfix1 ... vytvori novou lokalni vetev - kopii vzdalene vetve hotfig1  
git rebase master ... jako merge, ale není fast forward, feature branch A-B-C-D, master branch A-B-E-F, vysledek A-B-E-F-C-D
git merge master ... sjednoti zmeny - prijme zmeny z master do aktualni branche, feature branch A-B-C-D, master branch A-B-E-F, vysledek A-B-C-D-E-F  

### git vnitrnosti

git count-objects -v ... statistiky objektu  

### git flow

Po doinstalovani doplnku [flow](http://danielkummer.github.io/git-flow-cheatsheet/)
lze ridit vyvoj (management vice vetvi) jednodusseji.

### Vyreseni konfliktu

git checkout master  
git branch nova-vetev-na-ulozeni-konfliktnich-commitu  
git fetch --all  
git reset --hard origin/master  

### GitLab

[GitLab api - skupiny](https://docs.gitlab.com/ce/api/groups.html)  
[GitLab api - projekty](https://docs.gitlab.com/ee/api/projects.html)  
curl -k --header "PRIVATE-TOKEN: $TOKEN" https://gitlab.url.com/api/v3/groups/my-group 2>/dev/null | grep -o "[^,\"]\+:my-group/[^,\"]\+\.git" ... url na vylistovani objektu grupy  

### Scenare

##### procisteni .git adresare

Zdroj: [https://stackoverflow.com/questions/5613345/how-to-shrink-the-git-folder](https://stackoverflow.com/questions/5613345/how-to-shrink-the-git-folder):  
```
git clone remote-url
for branch in `git branch -a | grep remotes | grep -v HEAD | grep -v master`; do
    git branch --track ${branch##*/} $branch
done

#!/bin/bash
#set -x

# Shows you the largest objects in your repo's pack file.
# Written for osx.
#
# @see http://stubbisms.wordpress.com/2009/07/10/git-script-to-show-largest-pack-objects-and-trim-your-waist-line/
# @author Antony Stubbs

# set the internal field spereator to line break, so that we can iterate easily over the verify-pack output
IFS=$'\n';

# list all objects including their size, sort by size, take top 10
objects=`git verify-pack -v .git/objects/pack/pack-*.idx | grep -v chain | sort -k3nr | head`

echo "All sizes are in kB. The pack column is the size of the object, compressed, inside the pack file."

output="size,pack,SHA,location"
for y in $objects
do
    # extract the size in bytes
    size=$[^1]

[^1]: `echo $y | cut -f 5 -d ' '`/1024
    # extract the compressed size in bytes
    compressedSize=$[^2]

[^2]: `echo $y | cut -f 6 -d ' '`/1024
    # extract the SHA
    sha=`echo $y | cut -f 1 -d ' '`
    # find the objects location in the repository tree
    other=`git rev-list --all --objects | grep $sha`
    #lineBreak=`echo -e "\n"`
    output="${output}\n${size},${compressedSize},${other}"
done

echo -e $output | column -t -s ', '

git filter-branch --tag-name-filter cat --index-filter 'git rm -r --cached --ignore-unmatch filename' --prune-empty -f -- --all

rm -rf .git/refs/original/

git reflog expire --expire=now --all

git gc --prune=now

git gc --aggressive --prune=now
git push origin --force --all
git push origin --force --tags

#MIGRACE REPA
git clone --mirror REPO
git lfs install --local
git lfs migrate import --verbose --above=100MB --everything
git remote add github REPO2
git lfs fetch --all
git push github --mirror
git lfs push github --all

```
