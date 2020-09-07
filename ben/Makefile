export GO111MODULE=on
DB_HOST:=127.0.0.1
DB_PORT:=3306
DB_USER:=isucari
DB_PASS:=isucari
DB_NAME:=isucari

MYSQL_CMD:=mysql -h$(DB_HOST) -P$(DB_PORT) -u$(DB_USER) -p$(DB_PASS) $(DB_NAME)

NGX_LOG:=/tmp/access.log
MYSQL_LOG:=/tmp/slow-query.log

KATARU_CFG:=./kataribe.toml

SLACKCAT:=slackcat --tee --channel 2020_isucon_taisakushi
SLACKRAW:=slackcat --channel 2020_isucon_taisakushi

PPROF:=go tool pprof -png -output pprof.png http://localhost:6060/debug/pprof/profile

PROJECT_ROOT:=/home/isucon/isucari
BUILD_DIR:=/home/isucon/isucari/webapp/go
BIN_NAME:=isucari

CA:=-o /dev/null -s -w "%{http_code}\n"

pprof:
	$(PPROF)
	$(SLACKRAW) -n pprof.png ./pprof.png

setup:
  # sudo apt-get update
	sudo apt install -y percona-toolkit dstat git unzip snapd
	# git setup
	git config --global user.email "g5.taisa831@gmail.com"
	git config --global user.name "taisa831"
	# kataribe
	wget https://github.com/matsuu/kataribe/releases/download/v0.4.1/kataribe-v0.4.1_linux_amd64.zip -O kataribe.zip
	unzip -o kataribe.zip
	sudo mv kataribe /usr/local/bin/
	sudo chmod +x /usr/local/bin/kataribe
	rm kataribe.zip
	kataribe -generate
	# myprofiler
	wget https://github.com/KLab/myprofiler/releases/download/0.2/myprofiler.linux_amd64.tar.gz
	tar xf myprofiler.linux_amd64.tar.gz
	rm myprofiler.linux_amd64.tar.gz
	sudo mv myprofiler /usr/local/bin/
	sudo chmod +x /usr/local/bin/myprofiler
	# slackcat
	wget https://github.com/bcicen/slackcat/releases/download/v1.5/slackcat-1.5-linux-amd64 -O slackcat
	sudo mv slackcat /usr/local/bin/
	sudo chmod +x /usr/local/bin/slackcat
	slackcat --configure