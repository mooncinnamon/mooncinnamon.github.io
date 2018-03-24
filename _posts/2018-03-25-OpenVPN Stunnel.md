친구가 중국에 갔는데 제일 불편한게 VPN이라더라...

간단하게 공유기의 PPTP로 구성했지만 모바일에서는 막히고 OPENVPN은 사용불가가 떠서 검색을 해보니 몇개의 문서가 나왔다.

http://www.etnews.com/20170124000186

중국의 방화벽인 만리장성이 패킷을 막아서 그런다고 작성되어 있었다.



뭐... 그렇다면 중국에 전혀 VPN을 사용할 수 없어야 하는데 의외로 사용하는 사람들이 많았다.

https://www.top10bestvpn.com/?kw=china%20vpn&c=240626881917&t=search&p=&m=e&adpos=1t2&dev=c&devmod=&mobval=0&network=g&campaignid=232841651&adgroupid=19017215171&targetid=kwd-11645012743&interest=&physical=1009856&feedid=&ts=&utm_source=google&a=1033&gclid=CjwKCAjw7tfVBRB0EiwAiSYGM8KNNSTX8q440L2ixBOuuvVklkP7G3DWOZXhpgC1eBZyFsWADMEfYBoCqrkQAvD_BwE&gclsrc=aw.ds

[중국에서 사용하는 VPN목록]



그렇다면 크게 어렵지 않는 방법으로 만들 수 있다고 가정, 찾아보니 stunnel을 사용해서 패킷전체를 ssl 해버리면 된다는 글을 찾았다. 

stunnel 이외에도 ssh-tunneling, proxy등 방법은 많았으나, proxy는 속도가 걱정되고 ssh-tunneling은 사용자가 putty로 키기 애매할 것 같아서 stunnel로 구축했다.



stunnel은 이름 그대로 ssl-tunneling으로

client [ openvpn <-> stunnel ] ========= server [ stunnel <-> openvpn]

의 연결방식으로 동작하게 된다.

기존의 openvpn과의 차이점은 openvpn을 route로는 삼지만 직접 연결하는 부분은 localhost의 stunnel이고 stunnel끼리 연결이 수립되게 되면 openvpn 연결이 되는 구조로 되어있다.

기존의 사용하는 openvpn이 udp로 구성되어 있지만 stunnel을 사용하는 경우 패킷 손실이 심해지기 때문에 tcp 방식으로 openvpn을 작동시켜야 하고 도커를 사용해서 tcp용 openvpn docker를 하나 더 생성했다.



https://github.com/vimagick/dockerfiles/tree/master/openvpn

해당 이미지를 사용해서 구축했다.



docker-compose를 사용하기 때문에 서버에서는 크게 어려운 부분은 없으나, 클라이언트에서 연결수립 하는 방법이 좀 헷갈려서 설정 파일을 올려본다

```bash
pid = /usr/local/etc/stunnel/stunnel.pid
output = stunnel.log

compression = zlib
sslVersion = all

client = yes

[openvpn]
accept = 127.0.0.1:1194
connect = [Please Your Server IP]:4911
```

stunnel client 설정 파일이다.



openvpn 의 설정은 nopass로 ovpn의 파일을 만들어서 사용할시 몇가지 부분만 수정해 주면 되는데.



```bash
remote 127.0.0.1 1194 tcp

redirect-gateway def1

route [Please Your Server IP] 255.255.255.255 net_gateway
```



route 부분을 추가하고 remote 는 127.0.0.1 (localhost) 로 변경해주면 된다.