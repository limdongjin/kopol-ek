# kopol-ek
20대 국회 법안 (  ~ 의안번호2013519 ) 덤프 데이터를 ElasticSearch/Kibana에 넣어서 법안 분석 환경 구축하기. 

## Demo Image

![](/images/kibana-screen.png)

## Prerequisites

1. brew가 설치되어있거나 ruby가 설치되어있어야힘.
2. npm이 설치되어있어야함
3. macOS

# 1. ElasticSearh 설치 및 Kibana 설치

이미 ElasticSearch 와 Kibana가 설치되어있다면 이 단계는 스킵해도 무방하다.

```bash
# ruby가 기존에 깔려있는지 확인하자
ruby -v

# npm이 기존에 깔려있는지 확인하자
npm -v

# brew 설치
brew -v
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


# cask 설치
brew tap caskroom/cask
brew install brew-cask

# 자바 설치
brew cask install homebrew/cask-versions/java8

# 엘라스틱서치 설치
brew install elasticsearch

# 환경변수설정
echo 'export PATH="/usr/local/opt/elasticsearch/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile

# 잘 실행되는지 확인하기
elasticsearch # 브라우저로 127.0.0.1:9200

# kibana 설치
brew install kibana

# kibana가 잘 실행되는지 확인
kibana # 브라우저로 127.0.0.1:5601
```

## 2. 덤프 ElasticSearch에 bulk하기

```
# dump파일 다운로드
wget https://raw.githubusercontent.com/limdongjin/kopol-ek/master/dump00.json

# elasticdump 설치
npm install elasticdump -g

# dump
# 만약 elasticsearch 가 꺼져있다면 다시킨다.
elasticdump \
--input=dump.json \
--output=http://127.0.0.1:9200/koreabills
```

## 3. kibana 설정 및 완료!

1. Management-IndexPatterns 메뉴에서 Create Index Pattern클릭
2. Step 2 of 1: Define index Pattern => korea*
3. Step 2 of 2: Configure settings => I dont't want to use the Time Filter
4. Discover로 가서 확인
