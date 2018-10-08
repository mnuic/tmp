Odem na https://github.com/minus5/tmp i napravim fork.
Napravim clone, postavim si origin na $USER.
Ovo se obicno zove origin. Da bi bilo jasnie sto je cije ovdje cu koristi $USER i minus5.
U github open source svijetu uobicajeno je origin i upstream, ianic ($USER) i minus5 mi daju vise informacija.
```
cd ~/work/gocode/src/github.com/$USER
git clone git@github.com:$USER/tmp.git -o $USER
git branch -vva
```
dodam drugi remote (upstream)
```
git remote add minus5 git@github.com:minus5/tmp.git
git fetch minus5
```

pogledam sto imam
```
git branch -vva
```

radim...
```
git checkout master
git checkout -b {feature_branch}
```

povucem promjene koje su u medjuvremenu nastale
```
git fetch minus5
git checkout master
git merge minus5/master

git checkout {feature_branch}
git rebase master
```

kreiram pull request
```
git push -u ianic {feature_branch}
```
napisat ce mi url za pull request
odem tamo i posaljem pull request


Dalje nastavlja onaj koji merge-a.
To moze biti ista osoba isti repo, kao u nastavku.

pripremim se za merganje pull requesta
editiram .git/config
u sekciji [remote "minus5"] mu objasnim da mi skida i pull requeste
```
fetch = +refs/pull/*/head:refs/pull/minus5/*
```
napravim branch za merge
```
git checkout -b m5_master minus5/master
git config push.default upstream
```

testiram pull request
```
git fetch minus5   # dovucem pull requeste
git checkout -b 1 pull/minus5/1  # napravim branch od pull requeste
```
testiram taj branch ….

merge pull requesta
```
git checkout m5_master
git merge  pull/minus5/1
git push minus5 HEAD:master
```

nakon sto je merge-an aktualiziram svoj fork
```
git fetch minus5
git checkout master
git merge minus5/master
git push
```


Nakon sto sam prvi puta napravio sve pripreme dalje ide.

napravim pull request
```
git checkout master
git checkout -b f1 
…
git push -u ianic  f1
```
pull request na site (napise mi url)


merge pull requesta
```
git pull minus5   # napise mi da ima novi pull
git checkout m5_master
git merge pull/minus5/2
git push 
```

aktualiziram fork
```
git fetch minus5
git checkout master
git merge minus5/master
git push
```

Reference:
[Github Forking](https://gist.github.com/Chaser324/ce0505fbed06b947d962)
[Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches) *** required reading
[Push Config](https://stackoverflow.com/questions/24864700/fatal-the-upstream-branch-of-your-current-branch-does-not-match-the-name-of-you)
