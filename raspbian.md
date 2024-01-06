# 라즈베리파이 초기 설정
```
sudo apt update
sudo apt upgrade
```

## 한글깨짐
```
sudo apt-get install fonts-unfonts-core -y
sudo apt-get install ibus ibus-hangul -y
sudo reboot
```

## gcc 
```
vim 파일이름.c
gcc -o 실행파일이름 소스파일
./실행파일이름
```
## InfluxDB2 install
* InfluxDB download key using wget
```
  wget -q https://repos.influxdata.com/influxdata-archive_compat.key
  echo '393e8779c89ac8d958f81f942f9ad7fb82a25e133faddaf92e15b16e6ac9ce4c influxdata-archive_compat.key' | sha256sum -c && cat influxdata-archive_compat.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg > /dev/null
  echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
```
* Pakaes are up to data && install Influxdb2
  ```
  sudo apt-get update && sudo apt-get install influxdb2 -y
  ```
* error) can't find influxdb2 pakage
* * influxdb1 install
    ```
    sudo apt-get install influxdb -y
    ```

* InfluxDB as a backgroundservice on startup
  ```
  sudo service influxdb start
  ```
* InfluxDB is status(service)
  ```
  sudo service influxdb status
  ```
## Grafana install
* Repository's GPGkey +
```
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```
* Repository +
```
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```
* program install
```
sudo apt update
sudo apt install grafana
```
* program progress
```
sudo service grafana-server start
```
# 파이썬 네트워크 프로그래밍
## 타임 서버 프로그램
-> 소켓을 사용하여 TCP서버를 구성하는 과정
* socket()메소드 호출
```
import socket
sock = socket.socket(socket,AF_INET, socket.SOCK_STREAM)
```

sock은 socket클래스 객체이며 소켓 객체 메소드를 사용하여 필요한 기능을 수행한다. 생성된 소켓의 속성을 확인하려면 sock.family, sock.type, sock.proto속성을 조사한다. 각각 소켓의 주소 유형, 소켓 유형, 프로토콜 값을 나타낸다.



소켓 객체를 생성하고 난 다음엔 통신 종단점을 지정한다. 소켓을 생성할 때 AF_INEF유형을 지정하였으므로 통신 종단점은 (host, port)튜플로 나타낸다. host는 프로그램이 실행되고 있는 컴퓨터의 이름이나 IP주소를 문자열로 나타낸것이다. 종단점은 다음과 같이 정의할 수 있으며 반드시 튜플로 설정되어야한다.
```
address = ('', 5000)
```
생성된 소켓을 통신 종단점과 결합하고 listen()메소드를 호출하여 클라이언트의 연결을 기다린다. listen(5)에서 ()속의 숫자는 동시 연결 가능한 소켓 수이다.
```
sock.bind(address)
sock.listen(5)
클라이언트의 연결 요청을 받으면 accept()메소드를 이용하여 요청을 허용한다. accept()메소드는 연결 요청한 클라이언트의 소켓과 클라이언트 주소(ip, port)를 튜플로 반환한다. 연결된 클라이언트와의 통신은 accept()가 반환한 소켓을 통해 이루어진다.
```
client,addr = sock.accept()
```
위에서 client는 클라이언트 소켓이고, addr은 클라이언트 주소이다. 서버소켓 sock은 클라이언트와 연결을 받기위해 사용되고 실제 데이터 송수신은 클라이언트 소켓을 통해 이루어진다. 따라서 한개의 서버가 여러 개의 클라이언트와 통신이 가능하다.

클라이언트와 연결이 이루어졌으므로 send()함수를 이용하여 데이터를 보낼 수 있다. 전송 데이터는 바이트 형어야한다. 문자열을 바이트형으로 변환하려면 str.encode()메소드를 이용한다. 이 메소드는 문자열을 utf-8 코드를 사용하여 바이트형으로 변환한다.
```
client.send("message".encode())


아래 코드는 위 서버프로그램을 하나로 묶은 것이다.
```python
# time_server.py
import socket
import time
sock = socket.socket(socket.AF_INET,socket.SOCK_STREAM)#소켓 생성
address = ('', 5000)#종단점 주소
sock.bind(address)#주소와 소켓결합
sock.listen(5)#연결 대기

while True:
  client, addr = sock.accept()#연결허용. 클라이언트 소켓과 주소 반환
  print("Connection requested from",addr)
  client.send(time.ctime(time.time()).encode())#bytes형 메시지 전송
  client.close()#소켓 헤제
```
위 프로그램을 실행하고 명령창에서 "telnet localhost 5000"을 실행하면 현재 시간을 볼 수 있다.
