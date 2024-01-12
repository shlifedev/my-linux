# 노트북
개인 노트북 성능 최적화용 

## irqbalance 해제하기.
선택적 옵션
```sh
$ sudo service irqbalance stop 
```

## cpu 코어 최적화옵션
- 4코어 혹은 8코어로 쓰로틀링에 따라 제한했다.
- 2.4~2.5 ghz + 터보를 유지하는게 좋다.

## 언더볼팅
현재 설정한 값은 이렇다
```
temperature target: -2 (98C)
core: -75.2 mV
gpu: -99.61 mV
cache: -75.2 mV
uncore: -75.2 mV
analogio: -75.2 mV
powerlimit: 58.75W (short: 0.00244140625s - enabled) / 47.0W (long: 28.0s - enabled) [locked]
turbo: enable
```

따라서 언더볼팅은 다음과같이 하면 안정적이었다.
```sh
$ sudo undervolt --core -75 --gpu -100 --cache -75 --uncore -75 -analogio -75
```
### 자동 실행 등록
1. nano로 다음 경로에 서비스를 생성 `/etc/systemd/system/undervolt.service`
```                   
[Unit]
Description=undervolt
After=suspend.target
After=hibernate.target
After=hybrid-sleep.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/undervolt -v --core -75 --cache -75 --gpu-100 --uncore>

[Install]
WantedBy=multi-user.target
WantedBy=suspend.target
WantedBy=hibernate.target
WantedBy=hybrid-sleep.target
```
2. 서비스 등록
`$ systemctl enable undervolt`


