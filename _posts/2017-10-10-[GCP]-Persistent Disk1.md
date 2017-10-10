---
title : GCP, Persistent Disk (Activity Tracking)
description: Creating a Persistent Disk (Activity Tracking)
categories:
 - GCP
tags:
 - Qwiklab
 - GCP
---
>qwiklab 실습 중 파생된 정보 입니다.

## Intro
VM 인스턴스를 생성하고 persistent disk를 연결해 본다.

---
## Try
먼저 GCP 홈에서 **Cloud Shell** 을 실행합니다.
![](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10-10/%EC%BA%A1%EC%B2%98_2017_10_10_16_15_25_659.png?raw=true)

가상 머신이 로드되면 5GB의 영구 disk가 할당돼 있습니다.(기본)

자 , *Cloud Compute 인스턴스* 를 생성해 봅시다.
```sh
gcloud compute instances create gcelab --zone us-central1-c
```
- **gcelab** 이란 인스턴스가 생성합니다.

콘솔은 다음과 같은 결과를 보입니다.
```sh
Created [...].
NAME       ZONE           MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP EXTERNAL_IP    STATUS
gcelab us-central1-c n1-standard-1             10.240.X.X  X.X.X.X        RUNNING
```

다음, 영구 디스크를 생성합니다.
```sh
gcloud compute disks create mydisk --size=200GB \
--zone us-central1-c
```
- 기존 생성된 VM 인스턴스와 같은 *리전(resion)* 을 가져야 합니다.

만들어진 영구 디스크를 VM 인스턴스에 붙여보죠.
```sh
gcloud compute instances attach-disk gcelab --disk mydisk --zone us-central1-c
```

```sh
Updated [https://www.googleapis.com/compute/v1/projects/...].
```
- 위와 같은 출력이라면 성공적으로 수행한 것입니다.

<u>이제 붙인 영구 디스크를 일련의 device로써 사용이 가능합니다.</u>

이번엔 ssh를 설정하죠.
```sh
gcloud compute ssh gcelab --zone us-central1-c
```

자, 앞서 만들어진 영구 디스크는 VM 인스턴스 내에서 이렇게 확인할 수 있습니다.
```sh
ls -l /dev/disk/by-id/
```

다음과 같은 출력을 확인할 수 있습니다.
```sh
lrwxrwxrwx 1 root root  9 Feb 27 02:24 google-persistent-disk-0 -> ../../sda
lrwxrwxrwx 1 root root 10 Feb 27 02:24 google-persistent-disk-0-part1 -> ../../sda1
lrwxrwxrwx 1 root root  9 Feb 27 02:25 google-persistent-disk-1 -> ../../sdb
lrwxrwxrwx 1 root root  9 Feb 27 02:24 scsi-0Google_PersistentDisk_persistent-disk-0 -> ../../sda
lrwxrwxrwx 1 root root 10 Feb 27 02:24 scsi-0Google_PersistentDisk_persistent-disk-0-part1 -> ../../sda1
lrwxrwxrwx 1 root root  9 Feb 27 02:25 scsi-0Google_PersistentDisk_persistent-disk-1 -> ../../sdb
```
- 장치명은 VM 인스턴스에 붙일 때,  --device-name옵션을 통해 설정이 가능합니다.
- 기본 영구 디스크와 추가된 영구 디스크를 확인할 수 있습니다.

자, 이것을 사용하기 위해 마운트해야겠죠?
```sh
sudo mkdir /mnt/mydisk
sudo mkfs.ext4 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1
sudo mount -o discard,defaults /dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1 /mnt/mydisk
```
- 마운트 대상 디렉토리를 생성합니다.
- 영구 디스크의 File System을 ext4로 포맷합니다.
- 마운트를 수행합니다.

마지막으로 이 작업을 부팅시 마다 수행하게 설정합니다.
1. /etc/fstab 을 vi들을 통해 엽니다.
2. **UUID=** 라인을 찾습니다.
3. 다음의 코드를 값으로 설정합니다.
```sh
/dev/disk/by-id/scsi-0Google_PersistentDisk_persistent-disk-1 /mnt/mydisk ext4 defaults 1 1
```

---
## comment
1. Local SSD를 생성해 붙일 수도 있다.
2. 로컬 SSD를 통해 많은 장점을 가질 수 있다.
- Less than 1 ms of latency
- Up to 680,000 read IOPs and 360,000 write IOPs
      - IOPs : input output per second
3. 에러 등의 문제 시, data가 날라간다.
4. 대신 백업이 안 됨. 따로 백업을 구성해줘야함.
5. 로컬 SSD는 다음을 참고하자.
- [Adding Local SSD](https://cloud.google.com/compute/docs/disks/local-ssd#create_a_local_ssd)
