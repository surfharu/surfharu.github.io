---
title: Monitoring ethereum transactions using blockscout
author: surfharu
date: 2022-11-01 09:00:00 +0800
categories: [blockchain]
tags: [blockchain, ethereum, blockscout] # TAG names should always be lowercase
---

## blockscout 이란? 
이더리움 블록 및 트랜잭션을 모니터링 할 수 있는 오픈소스 프로젝트이다.
> [blockscout - Blockchain Explorer for inspecting and analyzing EVM Chains](https://github.com/blockscout/blockscout)

## 목표
blockscout 을 이용해 설치한 이더리움을 연결해 본다.

## blockscout 환경 설정
`docker-compose-blockscout.yml` 파일을 설정해 준다.  
blockscout이 사용할 db 경로, blockscout 환경 설정 파일 위치, 이더리움이 설치된 주소를 설정한다.
```yaml
version: '3.8'
services:
postgres:
image: postgres:13.4-buster
restart: always
container_name: 'postgres'
environment:
POSTGRES_PASSWORD: ''
POSTGRES_USER: 'postgres'
POSTGRES_HOST_AUTH_METHOD: 'trust'
volumes:
- ./data-postgres:/var/lib/postgresql/data
ports:
- 7432:5432
networks:
priv-block-net:
ipv4_address: 172.20.254.2
blockscout:
depends_on:
- postgres
image: blockscout/blockscout:${DOCKER_TAG:-latest}
restart: always
container_name: 'blockscout'
links:
- postgres:database
command: 'mix do ecto.create, ecto.migrate, phx.server'
env_file:
- ./common-blockscout.env
environment:
ETHEREUM_JSONRPC_VARIANT: 'geth'
BLOCK_TRANSFORMER: 'clique'
ETHEREUM_JSONRPC_HTTP_URL: http://192.168.161.25:8545/
DATABASE_URL: postgresql://postgres:@172.20.254.2:5432/blockscout?ssl=false
ports:
- 4000:4000
networks:
priv-block-net:
ipv4_address: 172.20.254.3
networks:
priv-block-net:
driver: bridge
ipam:
config:
- subnet: 172.20.254.0/28
```

## blockscout 실행
```bash
docker-compose -f docker-compose-blockscout.yml up -d
```

## blockscout 접속
브라우저에서 `http://localhost:4000` 주소로 접속한다.  
실시간으로 블록 및 트랜잭션 정보를 조회 할 수 있다. 

![](/assets/images/blockchain-1-1.png)