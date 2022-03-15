# 20220317examen

#Scripts git

## Rebase con interactive:

#!/usr/bin/env bash
git init
touch f1
git add f1
git commit -m "f1"
touch f2
git add f2
git commit -m "f2"
touch f3
git add f3
git commit -m "f3-este-commit-rompe"
touch f4
git add f4
git commit -m "f4-este-commit-rompe"
touch f5
git add f5
git commit -m "f5"
git --no-pager log --oneline --all 
#hasta aqui
git rebase --interactive <commit-antes-de-lo-que-queremos-borrar>
#cambiar 'pick' por 'drop'


##EXPLICACIÓN: Si solo una rama modifica un fichero, al
#mergear, esos cambios serán aceptados sin conflicto

rm -rf .git
rm f1
git init
echo "L1 en f1 en rama main" >> f1
git add f1
git commit -m "+f1:L1"
echo "L2 en f1 en rama main" >> f1
git add f1
git commit -m "+f1:L2"
git --no-pager log --oneline --all --graph
git checkout -b rama1
echo "L1 en f1 en rama1" >> f1
git add f1
git commit -m "+f1:L1"
echo "L2 en f1 en rama1" >> f1
git add f1
git commit -m "+f1:L2"
git checkout main
sed -i s/$/MOD/ f1
cat f1
git add f1
git commit -m "+f1:L1:L2:+MOD"
git merge --no-ff --no-edit rama1
git --no-pager log --oneline --all --graph

##Crear rama orphan

cd repository
git checkout --orphan orphan_name
git rm -rf .
rm '.gitignore'
echo "#Title of Readme" > README.md
git add README.md
git commit -a -m "Initial Commit"
git push origin orphan_name

##Git actions

name: GitHub Actions Demo
on: 
  push:
      branches: [ main ]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - name: Que ruta es
        run: pwd
      - run: echo "🍏 This job's status is ${{ job.status }}."

