---
title: github
---

## Odkazy

https://www.githubstatus.com/ ... Status zdraví služeb  

## GitHub akce

[GitHub akce](/automatizace/github)  

## GitHub markdown

[GitHub Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)  
[Barevný text](https://github.com/orgs/community/discussions/31570)  
[Vysouvací bloky](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/organizing-information-with-collapsed-sections)  
[emoji symboly](https://github.com/ikatyang/emoji-cheat-sheet/blob/github-actions-auto-update/README.md)  

## GitHub Copilot

### Adresářová struktura

.github/agents/*.agent.md  
.github/instructions/*.instructions.md  
.github/prompts/*.prompt.md ... předdefinované prompty  
.github/copilot-instructions.md ... instrukce, které si Copilot přečte při jakémkoli promptu v repozitáři  

### prompty

Explain this project  
What are the dependencies for running the a.sh  
@workspace /explain #file:  
/doc = generate inline code documentation for the selected code  
@workspace Generate a README.md file that can be used as a repo description  
@workspace /explain #file: How can I improve the readability of the selected code  
@workspace /explain #file: How can I improve the maintainability of the selected code  
@workspace /explain #file: How can I improve the modularity of the selected code  
@workspace /explain #file: How can I improve the exception handling of the selected code  
@workspace /explain #file: How can I improve the performance with the asynchronous tasks or methods in the file  
@workspace /explain #file: How can I protect the sensitive data in this class  
@workspace /explain #file: How can I decrease complexity of the selected code  
Can you please write a terraform script that deploys azure web app with deployment slots  
Can you add code comments into the script?  
Can you add inline comments in this file?  
Add JSDoc comments for the TaskManager function?  
Refactor the code in the file. Add the inline comment explaining the purpose of the refactored code  
Create usage examples or descriptions for the class and its methods  
Can you fix the bugs in the code?  
/tests  
Can you please generate unit test with terratest?  
Convert the current file from json to yaml format  

### VSCode Copilot zkratky

ctrp-enter ... otevře okno pro doplňování kódu  

## Repozitáře

.github ... speciální repozitář, který slouží jako vzor pro nové repozitáře  

### Konfigurační soubory v repozitáři

.github/ISSUE_TEMPLATE/ ... vzory pro Issues  
.github/workflows/ ... Definice GitHub akcí  
.github/dependabot.yml ... konfigurace pro Dependabot  
.github/CODEOWNERS ... určuje skupiny, které budou automaticky  
.github/PULL_REQUEST_TEMPLATE.md ... vzor pro pull request  
.github/CONTRIBUTING.md ... pravidla pro editory repozitáře  
.github/SECURITY.md ... popis bezpečnostních pravidel  
.github/SUPPORT.md ... popis kanálů, jak žádat o podporu  
.github/FUNDING.md ... vytvoří "Sponzor" tlačítko viditelné nahoře, seznam odkazů na sponzorské platformy  
.github/linters/
## GH - GitHub CLI

gh alias set iv 'issue view --comments' ... vytvoření aliasu  
gh iv https://github.com/a/b/issues/4 ... použití aliasu, zobrazení komentářů pro issue 5  
gh issue view --comments https://github.com/a/b/issues/4 ... zobrazení komentářů pro issue 5  
gh repo list  ORG -L 300 --json name,repositoryTopics | jq '.[] | select(.repositoryTopics != null)' ... vylistuje repozitáře organizace ORG, které mají nadefinovaný nějaký topic (jak tag)  
gh repo set-default ORG/repo ... nastaví výchozí repozitář - mohu pal přímo pracovat s pull requesty, issues, konfigurací atd  
gh org list ... seznam organizací  
gh pr list ... seznam pull requestů  
gh pr view 462 ... zobrazí PR 462  
gr pr review 8 -a -R https://github.com/organizace/repozitar ... schválí pull request v daném repu  
gh pr merge 462 ... mergne PR 462  
gh run list ... reznam běhů akcí  
gh workflow list ... seznam akcí - workflow  

### GH API

gh api -X GET 'orgs/MYORG/teams/TEAM/members' -F per_page=100 --paginate --ca --jq '[.[].login] | map("involves:\(.)") | join(" ")' ... volání api, neřeším token jak v CURLu, použiji nativně jq zpracování  
gh api "orgs/MYORG/teams?per_page=150" ... seznam týmů  
gh api teams/17505467 ... informace o týmu s týmID xxx  

=== GH CLI v GH Akcích ===

```
steps:
  - name: Auto-merge nových PR
    run: gh pr merge --auto --merge "$PR_URL"
    env:
      PR_URL: ${{github.event.pull_request.html_url}}
      GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}
```

```
- name: Vytvoření releasu, přiložení souborů
  run: |
    tagname="${GITHUB_REF#refs/tags/}"
    gh release create "$tagname" dist/*.tgz
  env:
    GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}
```
