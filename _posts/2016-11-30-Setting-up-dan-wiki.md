---
title: Heroku - Old dan.wiki configuration
date: 2016-11-30 02:58:00 -500
categories: ['heroku','programming'] 
tags: ['technology']
---

`  21  cd SSH`\

`  22  ls`\

`  23  nano EC21.sh `\

`  24  sh EC21.sh `\

`  25  heroku --version`\

`  26  wget -O- `[`https://toolbelt.heroku.com/install-ubuntu.sh`](https://toolbelt.heroku.com/install-ubuntu.sh)` | sh`\

`  27  heroku --version`\

`  28  heroku`\

`  29  ls`\

`  30  cd Dropbox/`\

`  31  ls`\

`  32  cd Web\ Development/`\

`  33  ls`\

`  34  cd dan.wiki/`\

`  35  ls`\

`  36  mkdir heroku`\

`  37  cd heroku/`\

`  38  ls`\

`  39  cd mediawiki/`\

`  40  ls`\

`  41  composer update`\

`  42  git init`\

`  43  git add .`\

`  44  git commit -m "first"`\

`  45  git config --global user.email "omitted@omitted.com"`\

`  46  git config --global user.name "Dan"`\

`  47  git commit -m "first"`\

`  48  git push heroku master`\

`  49  heroku `[`git:remote`](git:remote)` -a danwiki`\

`  50  git push heroku master`\

`  51  git add ./images/logo.png`\

`  52  git commit -m "logo"`\

`  53  git push heroku master`\

`  54  heroku open bash`\

`  55  heroku run bash`\

`  56  ls`\

`  57  nano LocalSettings.php `\

`  58  git add LocalSettings.php`\

`  59  git commit -m "LocalSetting.php"`\

`  60  git push heroku master`\

`  61  git add LocalSettings.php`\

`  62  nano LocalSettings.php `\

`  63  git add .`\

`  64  git commit -m "googleAnalytics"`\

`  65  git add extensions/googleAnalytics/`\

`  66  git commit -m "googleAnalytics"`\

`  67  git add extensions/googleAnalytics/*`\

`  68  git add extensions/googleAnalytics/*.*`\

`  69  git add extensions/googleAnalytics`\

`  70  git commit -m "googleAnalytics"`\

`  71  git add extensions`\

`  72  git commit -m "googleAnalytics"`\

`  73  git add extensions/.`\

`  74  git commit -m "googleAnalytics"`\

`  75  git commit -am "googleAnalytics"`\

`  76  git add .`\

`  77  git commit -am "googleAnalytics"`\

`  78  git add *`\

`  79  git commit -am "googleAnalytics"`\

`  80  ls -la`\

`  81  cd .git/`\

`  82  ls`\

`  83  cd ..`\

`  84  ls`\

`  85  ls -la`\

`  86  ls -lah`\

`  87  git status`\

`  88  git commit -a`\

`  89  git add`\

`  90  git add -A .`\

`  91  git status`\

`  92  cd extensions/googleAnalytics/`\

`  93  ls`\

`  94  ls -la`\

`  95  rm .git`\

`  96  rm -rf .git`\

`  97  ls -la`\

`  98  rm .git*`\

`  99  ls`\

` 100  ls -la`\

` 101  cd ..`\

` 102  ls`\

` 103  git add .`\

` 104  git status`\

` 105  git add -A .`\

` 106  git status`\

` 107  git add extensions/googleAnalytics/`\

` 108  git status`\

` 109  git commit -am "googl"`\

` 110  git push heroku master`\

` 111  git add extensions/.`\

` 112  git commit -am "googl"`\

` 113  cd extensions/`\

` 114  ls`\

` 115  mv googleAnalytics/ googleAnalytics1`\

` 116  mv googleAnalytics1/ googleAnalytics`\

` 117  cd ..`\

` 118  ls`\

` 119  git add .`\

` 120  git commit -m "g"`\

` 121  git ls-files extensions/googleAnalytics/`\

` 122  git push heroku master -f`\

` 123  git add extensions/googleAnalytics/*`\

` 124  git add --force extensions/googleAnalytics/`\

` 125  git commit -m "g"`\

` 126  ls -la`\

` 127  cd .git`\

` 128  ls`\

` 129  nano index`\

` 130  cd branches/`\

` 131  ls`\

` 132  cd ..`\

` 133  l`\

` 134  ls`\

` 135  cd objects/`\

` 136  ls`\

` 137  cd ..`\

` 138  ls`\

` 139  cd refs/`\

` 140  s`\

` 141  ls`\

` 142  cd ..`\

` 143  ls`\

` 144  cd ..`\

` 145  git show submodules`\

` 146  git submodules`\

` 147  git submodule`\

` 148  cd ..`\

` 149  ls`\

` 150  cd ..`\

` 151  s`\

` 152  ls`\

` 153  cd googleAnalytics/`\

` 154  ls`\

` 155  rm gitinfo.json `\

` 156  rm -rf .git`\

` 157  rm .git*`\

` 158  cd ..`\

` 159  ls`\

` 160  mv googleAnalytics heroku/mediawiki/extensions/`\

` 161  cd heroku/mediawiki/`\

` 162  git add .`\

` 163  git status`\

` 164  mv extensions/googleAnalytics/ gAnalytics`\

` 165  git add .`\

` 166  git status`\

` 167  cd extensions/`\

` 168  ls`\

` 169  cd ..`\

` 170  ls`\

` 171  mv gAnalytics/ extensions/googleAnalytics`\

` 172  git add .`\

` 173  git status`\

` 174  git commit -m "yay"`\

` 175  git push heroku master`\

` 176  nano LocalSettings.php `\

` 177  git add .`\

` 178  ls`\

` 179  git status`\

` 180  git commit -m "logo fix"`\

` 181  git push heroku master`\

` 182  ls`\

` 183  cd ..`\

` 184  ls`\

` 185  cd ..`\

` 186  ls`\

` 187  cd Backups/`\

` 188  ls`\

` 189  cd Main\ Page/`\

` 190  ls`\

` 191  cd ..`\

` 192  l`\

` 193  ls`\

` 194  cd ..`\

` 195  ls`\

` 196  cd ..`\

` 197  ls`\

` 198  cd dan.wiki/`\

` 199  log`\

` 200  changelog`\

` 201  historu`\

` 202  history`\

` 203  cd ~`\

` 204  ls`\

` 205  cd Dropbox/Web\ Development/dan.wiki/`\

` 206  ls`\

` 207  cd heroku/`\

` 208  ls`\

` 209  cd mediawiki/`\

` 210  ls`\

` 211  git add .`\

` 212  git commit -m "wikidump"`\

` 213  nano LocalSettings.php `\

` 214  cd images/`\

` 215  ls`\

` 216  nano README `\

` 217  cp logo.png ..`\

` 218  ls`\

` 219  cd ..`\

` 220  ls`\

` 221  git add .`\

` 222  git commit -m "wikidump"`\

` 223  git push heroku master`\

` 224  nano LocalSettings.php `\

` 225  git add .`\

` 226  git commit -m "wikidump"`\

` 227  git push heroku master`\

` 228  heroku domains`\

` 229  heroku domains:add www.dan.wiki`\

` 230  nano LocalSettings.php `\

` 231  git add .`\

` 232  git pull heroku master`\

` 233  git status`\

` 234  git commit -m "localsettings"`\

` 235  git push heroku master`\

` 236  heroku domains:add `[`https://dan.wiki`](https://dan.wiki)\

` 237  nano LocalSettings.php `\

` 238  git add .`\

` 239  git commit -m "localsettings"`\

` 240  git push heroku master`\

` 241  heroku domains:remove www.dan.wiki`\

` 242  heroku plugins:install `[`https://github.com/naaman/heroku-vim`](https://github.com/naaman/heroku-vim)\

` 243  nano LocalSettings.php `\

` 244  git add .`\

` 210  ls`\

` 211  git add .`\

` 212  git commit -m "wikidump"`\

` 213  nano LocalSettings.php `\

` 214  cd images/`\

` 215  ls`\

` 216  nano README `\

` 217  cp logo.png ..`\

` 218  ls`\

` 219  cd ..`\

` 220  ls`\

` 221  git add .`\

` 222  git commit -m "wikidump"`\

` 223  git push heroku master`\

` 224  nano LocalSettings.php `\

` 225  git add .`\

` 226  git commit -m "wikidump"`\

` 227  git push heroku master`\

` 228  heroku domains`\

` 229  heroku domains:add www.dan.wiki`\

` 230  nano LocalSettings.php `\

` 231  git add .`\

` 232  git pull heroku master`\

` 233  git status`\

` 234  git commit -m "localsettings"`\

` 235  git push heroku master`\

` 236  heroku domains:add `[`https://dan.wiki`](https://dan.wiki)\

` 237  nano LocalSettings.php `\

` 238  git add .`\

` 239  git commit -m "localsettings"`\

` 240  git push heroku master`\

` 241  heroku domains:remove www.dan.wiki`\

` 242  heroku plugins:install `[`https://github.com/naaman/heroku-vim`](https://github.com/naaman/heroku-vim)\

` 243  nano LocalSettings.php `\

` 244  git add .`\

` 245  git commit -m "localsettings"`\

` 246  git push heroku master`\

` 247  heroku addons:open pointdns`\

` 248  nano LocalSettings.php `\

` 249  git add .`\

` 250  git commit -m "localsettings"`\

` 251  git push heroku master`\

` 252  heroku domains`\

` 253  nano LocalSettings.php `\

` 254  git add .`\

` 255  git commit -m "localsettings"`\

` 256  git push heroku master`\

` 257  nano LocalSettings.php `\

` 258  heroku domains:remove dan.wiki`\

` 259  heroku domains:add *.dan.wiki`\

` 260  nano LocalSettings.php `\

` 261  git add .`\

` 262  git commit -m "localsettings"`\

` 263  git push heroku master`\

` 264  nano LocalSettings.php `\

` 265  git add .`\

` 266  git commit -m "localsettings"`\

` 267  git push heroku master`\

` 268  nano LocalSettings.php `\

` 269  git add .`\

` 270  git commit -m "localsettings"`\

` 271  git push heroku master`\

` 272  heroku domains`\

` 273  nano LocalSettings.php `\

` 274  heroku domains:add dan.wiki`\

` 275  heroku domains:remove dan.wiki`\

` 276  nano LocalSettings.php `\

` 277  git add .`\

` 278  git commit -m "localsettings"`\

` 279  git push heroku master`



[Category:Category: Heroku]

