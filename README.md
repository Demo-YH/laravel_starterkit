# dockerで環境構築検討用(starter kit試す目的)  
## 環境  
<img alt="Static Badge" src="https://img.shields.io/badge/wsl2-w?style=plastic&logo=linux&logoColor=000000&labelColor=%23FCC624&color=%23FCC624"> <img alt="Static Badge" src="https://img.shields.io/badge/ubuntu-u?style=plastic&logo=ubuntu&logoColor=%23ffffff&labelColor=%23E95420&color=%23E95420"> <img alt="Static Badge" src="https://img.shields.io/badge/debian-l?style=plastic&logo=debian&logoColor=ffffff&labelColor=A81D33&color=A81D33">  
<img alt="Static Badge" src="https://img.shields.io/badge/Docker-d?style=plastic&logo=docker&logoColor=%23ffffff&labelColor=%232496ED&color=%232496ED">
<img alt="Static Badge" src="https://img.shields.io/badge/NGINX-n?style=plastic&logo=nginx&logoColor=%23ffffff">
<img alt="Static Badge" src="https://img.shields.io/badge/MySQL-m?style=plastic&logo=mysql&logoColor=%23ffffff&labelColor=%234479A1&color=%234479A1">
<img alt="Static Badge" src="https://img.shields.io/badge/php-p?style=plastic&logo=php&logoColor=%23ffffff&labelColor=%23777BB4&color=%23777BB4">
<img alt="Static Badge" src="https://img.shields.io/badge/livewire-w?style=plastic&logo=livewire&logoColor=%23ffffff&labelColor=%234E56A6&color=%234E56A6">  
<img alt="Static Badge" src="https://img.shields.io/badge/Laravel12-l?style=plastic&logo=laravel&logoColor=%23ffffff&labelColor=%23FF2D20&color=%23FF2D20">
<img alt="Static Badge" src="https://img.shields.io/badge/bun-b?style=plastic&logo=bun&logoColor=%23ffffff&labelColor=%23000000&color=%23000000">
<img alt="Static Badge" src="https://img.shields.io/badge/bootstrap-b?style=plastic&logo=bootstrap&logoColor=%23ffffff&labelColor=%237952B3&color=%237952B3">
<img alt="Static Badge" src="https://img.shields.io/badge/vite-v?style=plastic&logo=vite&logoColor=%23ffffff&labelColor=%23646CFF&color=%23646CFF">  


## 構築手順  
#### 1. wsl使用の為、仮想マシン プラットフォームを有効化  
####  (wslがインストールされていない場合:Linuxカーネル更新プログラムパッケージを  
####  インストールする)  
#### 2. wsl --set-default-version 2 コマンドでLinuxを標準でWSL2上で動くように設定  
#### 3. wsl --list --verbose　コマンドでLinuxがWSL1とWSL2のどちらで動いているかを確認  
#### 4. ubuntuをインストール  
#### 5. terminalにてアカウント作成  
#### 6. 任意のフォルダ作成  
#### 7. Docker Desktopインストール  
#### 8. dockerでwslを使用する設定に変更  
#### 9. terminalに戻りdockerで使用するイメージのフォルダ構成作成  
#### 10. Dockerfileにて、使用するイメージ作成の設定  
#### 11. composer.ymlにて作成するコンテナの初期状態を  
#### 「ports:」「volumes:」などYAML形式を用いて定義。  
#### 12. その他の使用するイメージの設定ファイル(my.cnf、default.conf)作成  
#### 13. docker compose up -d　コマンドを実行してコンテナの作成・起動  
#### 14. docker exec -it conteinerID bashでコンテナにはいる  
#### 15. 以降はLaravel12の環境構築  
#### ※bunインストールがalpineだとうまくいかなかった為、今回はphp-fpm(debian)を使用
#### 16. composer global require laravel/installer　コマンドでLaravelインストーラーをインストール  
#### 17. export PATH=$HOME/.composer/vendor/bin:$PATH　コマンドでlaravelコマンドを使用するためのパスを通す
#### 18. source ~/.bashrc　コマンドで変更状態を反映させる
#### ※スターターキットをDocker環境で構築したかったので、上記手順でLaravelプロジェクトの作成となる  
#### ※Livewireスターターキットを選択すると、flux(resources/views/flux)も入ってる  
#### 19. laravel new example　コマンドでLaravelのプロジェクトを作成  
#### 20. スターターキットの選択  
#### ※使用したいpackageを選択する  
#### ※npm installの実行はしない、bunを使用する為(npm選択する場合はbunをインストールしない)  
#### ※エラー：failed to open stream: Permission denied  
#### chmod -R 777 storage　コマンドで解消  
#### 21. cd example　コマンドでディレクトリ移動
#### 22. composer require --dev "squizlabs/php_codesniffer=*"　コマンドでPHP_CodeSniffierのインストール  
#### 23. bun install　コマンドでbunインストール(npm選択した場合は、この手順は行わない)  
#### 24. bun run build　コマンド実行(npm選択した場合は、この手順でなくnpmの実行を行う)  
#### 25. mysql使用の為、".env"の下記内容を修正
#### DB_CONNECTION=mysql　sqlite→mysql  
#### DB_HOST=127.0.0.1　使用しているdb名に修正  
#### DB_HOST以降からDB_PASSWORDまでのコメントアウト解除及び、自身で設定した内容への修正を行う  
#### 26. php artisan migrate　コマンドでマイグレーション  
#### 27. .env、config/app.phpにて言語設定変更  
#### 28. composer require askdkc/breezejp --dev　コマンドで翻訳ファイル取得  
#### 29. php artisan breezejp　コマンドで日本語設定  
#### ※laravel12再度表示確認  
#### ※個人お試し用以外での用途は非推奨  
## git cloneg後  
#### 1. docker exec -it conteinerID bashでコンテナにはいる  
#### 2. cd example　コマンドでディレクトリ移動  
#### 3. composer update　コマンド実行でautoload.php作成  
#### 4. cp .env.example .env　コマンドで.env作成  
#### 5. php artisan key:generate　コマンド実行  
#### 6. php artisan migrate　コマンド実行でdb再度作成  
#### 7. bun install　コマンドでbunインストール  
#### 8. bun run build　コマンド実行  
## 所感  
#### 頑張らなくても素敵レイアウトｗｗ  
#### dockerで使用するにはDockerfileの無いよう考えるの面倒くさい(楽なやり方あるのかもしれないけど)