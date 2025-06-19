# Boundless_Korea
- Bento + Broker 노드 설치

## 하드웨어, 소프트웨어 요구사항
- CPU 16쓰레드, >3Ghz
- RAM 32GB
- 최소 NVIDIA GPU with >= 8GB of VRAM / 권장 4090, 5090, L4
- SSD 200GB
- Ubuntu 20.04/22.04
- Base, ETH sepolia RPC [Alchemy](https://www.alchemy.com/)
- Base, ETH sepolia ETH [Alchemy](https://www.alchemy.com/faucets/base-sepolia)

## Bento + Broker 노드 설치

#### 패키지 설치 & 업데이트
```
sudo apt update && apt upgrade -y
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev tar clang bsdmainutils ncdu unzip libleveldb-dev libclang-dev ninja-build -y
```

#### Boundless Repo 복제
```
git clone https://github.com/boundless-xyz/boundless
cd boundless
git checkout release-0.10.1
```

#### Dependecies 설치
```
sudo ./scripts/setup.sh
```
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  
source "$HOME/.cargo/env"  
rustup update  
```
```
curl -L https://risczero.com/install | bash  
source ~/.bashrc  
rzup --version  
rzup install rust  
rzup install cargo-risczero  
```
```
curl -L https://foundry.paradigm.xyz | bash
source ~/.bashrc
foundryup
forge build
```
```
cargo install --git https://github.com/risc0/risc0 bento-client --bin bento_cli  
cargo install --locked boundless-cli  
```
```
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc  
source ~/.bashrc  
```
#### 테스트 proof 실행
```
just bento
```
```
RUST_LOG=info bento_cli -c 32
```
![image](https://github.com/user-attachments/assets/6d369ca8-530f-4b63-a9d3-77a0725812dc)
- 제대로 작동하면 다음과 같은 내용이 표시됨

----------------------------------------------------------------------------------------


#### 네트워크 
- Base Mainnet, Base Sepolia, Ethereum Sepolia 지원
- Alchemy	사용 [링크](https://www.alchemy.com/)

#### 공식 환경 파일(.env) 구성
.env.base  → Base Mainnet

.env.base-sepolia → Base Sepolia

.env.eth-sepolia → Ethereum Sepolia

- 원하는 네트워크에 따라 해당 파일을 수정해 사용

#### .env.base-sepolia 파일 설정
- 여기선 Base sepolia로 진행
```
nano .env.base-sepolia
```
```
export RPC_URL=""     # RPC URL을 "" 사이에 입력
export PRIVATE_KEY=   # EVM 지갑 개인 키 설정
```
- 위 코드 추가후 crtl + o -> crtl + x
```
source .env.base-sepolia
```
#### USDC facuet & deposit
- https://faucet.circle.com/
```
boundless account deposit-stake 10
```
#### Broker 실행
```
just broker
```
#### Broker 로그 확인
```
just broker logs
```
![image](https://github.com/user-attachments/assets/18e73816-19ff-4860-8c84-e08589c6decb)
- 이런식의 로그가 나오면 성공!!
- https://explorer.beboundless.xyz/provers
- 여기에 지갑 주소 넣고 나중에 확인해보기




