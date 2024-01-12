# 노트북
개인 노트북 성능 최적화용 

## irqbalance 해제하기.
선택적 옵션
```sh
sudo service irqbalance stop 
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
sudo undervolt --core -75 --gpu -100 --cache -75 --uncore -75 -analogio -75
```

