# EOS CHROME Burn & Earn Implementation 

**DEC 12, 2018**

<!-- MarkdownTOC depth=4 autolink=true bracket=round list_bullets="-*+" -->

# Abstract
현재 EOS에는 투표에 대한 비용이 존재하지 않고 이익 또한 존재하지 않는다. 사용자들의 자발적 참여에 BP 투표를 의지하고 있는 상황이다. 
EOS 투표의 중앙화 문제를 해결하기 위한 새로운 대안으로 EOS CHROME은 Burn & Earn Delegated DPOS(B&E DPOS)를 제안한다. 
B&E DPOS에는 BP 투표에 대한 비용과 이익이 존재한다. 만약 투표의 이익이 비용보다 높다면 더 많은 사용자들이 투표를 하게 될 것이며, 
반대의 경우엔 투표율이 줄어들게 될 것이다. B&E DPOS를 사용하여 우리는 사용자의 비용과 이익을 고려하여 투표에 대한 정교한 유인 체계를 설계할 수 있다. 

# Structure
## EOS CHROME(CR) to CHROMITE(CRM) trade

B&E DPOS가 작동하기 위해서 EOS CHROME(CR)코인은 내부 거래소 혹은 뱅커 알고리즘을 통해 CHROMITE(CRM)코인으로 교환 되어야 한다. 초기에 내부 거래소를 바로 도입하기에는 무리가 있다. 이유인 즉 슨, 충분한 유동성이 확보되지 않은 상황에서 내부 거래소를 두어 100% 시장의 힘으로 EOS CHROME – CHROMITE의 비율이 결정 되도록 방치하는 것은 초기 생태계 형성에 큰 걸림돌이 될 수 있기 때문이다. 따라서, 뱅커 알고리즘을 사용하여 CR – CRM 교환을 구현하는 것을 목표로 한다. 테스트를 위해 뱅커 알고리즘의 Connector Weight은 100%로 고정하여 1:1 교환을 구현해 보고 이후 CW = 50%로 조절하여 뱅커 릴레이를 구현해 볼 것이다. 
뱅커 알고리즘 또는 뱅커 릴레이로 CR – CRM 교환을 구현하면 다음과 같은 장점을 얻을 수 있다. 첫째로, Orderbook과 같은 오버 헤드가 큰 정보를 관리하지 않고도 실시간 시장 상황에 따른 가격 변동을 반영할 수 있다. 둘째로, 거래에 딜레이가 발생하지 않는다. 유동성이 낮은 거래소의 경우에 사용자는 거래 체결을 위해 오랜 시간 기다려야 할 수도 있다. 하지만 뱅커 알고리즘의 경우에는 이러한 딜레이가 발생하지 않는다. CR을 입금하면 곧바로 시장가가 계산이 되어 CRM이 지급되게 된다. 

## CHROMITE(CRM) to Voting 

EOS CHROME 블록체인 설계에는 돈으로 교환을 하는 CR 코인과 플랫폼 내에 투표와 DAPP Coin 구매를 위해 사용하는 CRM 코인이 존재한다. 
이 부분에선 CRM코인이 어떤 방식으로 투표에 사용될 수 있을지, 그리고 DAPP Coin구매에 어떤 방식으로 사용될 수 있을지에 대해서 논의 해보고자 한다. 

최초의 CRM 사용 방법은 다음과 같다. CRM을 가지고 있는 사용자들이 CRM을 Burn하게 되면 15-30개의 투표권을 갖게 된다. 
이후, 투표권을 가지고 자신에게 유익한 서비스를 제공하는 BP후보에게 투표를 진행 한다. 
BP투표를 많이 받은 BP 후보는 상위 21위 혹은 상위 60위 BP로 선정이 되어 BP로서 역할을 수행할 수 있다. 
사용자는 BP투표에 대한 대가로 해당 BP가 진행하고 있는 DAPP Project의 DAPP Coin을 받을 수 있다. 

여기서 투표의 Half-life 문제가 발생한다. 투표의 half-life는 투표의 반감기로 해석될 수 있다. 
투표의 반감기란 투표 영향력이 매년 마다 반으로 줄어드는 것을 말한다. BP투표에 있어서 이러한 장치를 둔 까닭은 BP의 고착 효과 lock-in effect를 막기위한 것으로 사료 된다.
따라서, 사용자는 주기적으로 BP를 투표함으로써 투표 파워를 새로 갱신할 수 있다. 

현재 EOS는 사용자가 BP 투표를 진행하기 위해서 자신이 보유한 EOS를 Staking하는 방식을 사용하고 있다. 
따라서, 사용자의 account 별로 투표 영향력을 확인할 수 있다. 예를 들어, 1개의 EOS를 내 계좌에서 다른 사람의 계좌로 보내려고 할 때 
EOS 블록체인 CPU와 Bandwidth를 사용하게 된다. 이더리움의 경우에는 이러한 네트워크 사용료를 수수료를 지불하는 방식으로 운영한다. 
반면, 이오스는 1개의 이오스를 보낸다고 가정할 때 5-6개정도의 EOS를 네트워크에 Staking해 두어야만 “무료”로 1개의 이오스를 전송할 수 있다. 
결국 5-6개를 이오스 블록체인에 걸어둔다는 것이 기회비용이기 때문에 완벽한 “무료”는 아니지만, 
사용자의 입장에서 이오스의 개수가 보낸 1개의 이오스 외에 줄어드는 것이 없기 때문에 직접적인 비용으로 인식하지 못한다.

BP투표도 유사한 방식으로 이루어 진다. 내가 보유한 이오스로 BP투표를 진행하기 위해서 보유한 모든 이오스 코인을 블록체인에 Staking해 두어야만 한다. 
따라서 내가 언제 얼만큼의 이오스를 Staking했는지에 대한 정보는 내 개인 account에 귀속 되는 것이고, 이 정보를 기반으로 투표의 반감기를 사용자 마다 
다르게 적용할 수 있다. 이 정보는 내 이오스를 Staking해서 얻은 RAM (Storage)에 특정 부분이 할당되어 저장되게 된다. 
정리하자면, 현재 EOS에는 Staking 기능이 있기 때문에 각 account가 진행한 BP투표에 대한 정보를 개인이 비용 부담을 하여 저장한다. 
그리고 이 정보를 기반으로 투표의 반감기를 적용할 수 있다. 

반면, EOS CHROME에서 진행하는 B&E DPOS는 CRM이 Staking되는 것이 아니라 소각이 되어 사라진다. 이후 소각된 reference 정보가 BP 투표에 사용되며 그에 따른 DAPP Coin 분배가 이루어 진다. 
EOS CHROME 의 B&E DPOS는 CRM가 투표를 진행할 때마다 사라지기 때문에 투표 반감기를 적용하기 위해 개인이 소각한 일시와 수량을 저장할 수 없다. 
따라서, 이 정보를 전부 취합하여 블록체인 상에서 관리한다는 것은 장기적으로 매우 큰 오버헤드를 야기할 수 있다. 
따라서, EOS CHROME B&E DPOS에선 투표를 받은 BP들의 Account로 투표 정보가 취합 되어 관리된다. 
UTC+9 기준 매일 00:00시에 현재까지 지급받은 투표수를 취합하여 Moving Average Computation 방식으로 투표와 투표 영향력 차감이 진행된다. 

이를 진행하기 위한 전반적인 Structure는 다음과 같다: 

 <img align="center" src="https://github.com/eosCHROME/Documentation/blob/master/KR/image/Burn%26Earn%20Structure%20ver0.01.jpg" width="800px" height="500px" />

User가 CRM를 "Burn"하게 되면 CRM은 EOSIO.BNE로 보내지게 되며 EOSIO.BNE multi-index table에 유입된 CRM정보가 기입된다. 
Index table 구성은 BP이름, 시간과, 보내진 CRM에 대비하여 기록되는 투표 양이 기록되게 된다. Data Storgae amount는 BP의 수(N)과 투표 저장 기간(T)의 곱으로 결정 된다. 이후 UTC+9hr(잠정)기준 매 24시간마다 취합된 CRM 양을 index table에 기록하게 된다. 이후 투표의 영향력은 index table의 entry를 하나씩 삭제하는 방식으로 진행 된다. Adjustmnet Period는 보다 정교한 emperical adjustment가 필요하다. 

## 개발 Roadmap 및 진행 상황 Update 2018.12.18

1. eosio.burn contract initial draft completed
- The development for CR transfer to individual BP and sorting/ranking based on the received CR has been completed. 
- Further implementations: 
- (1) CR to thirty different voting rights that can be used to elect 30 different BPs. 
- (2) receiving BP-dAPP coins as a result of voting 
- (3) 30-day moving average table segmented in 24 hours (GMT+9) to avoid Denial of Service and unnecessary overhead in keeping track of BP voting 

2. Resource Allocation
- option 1: Allocating resources based on received CRM in BP reserve pool -> Pitfall: How will users use computer resources? 
- option 2: Everyone to lock CRM when using computer resources. i.e BPs, Users, Dapp developers must stake CRM to use resources. For users they have two options when it comes to using CRM. (1) Voting BP and earn rewards. (2) Staking and using hardware resources. 
- option 3: Allowing CR locking rather than CRM locking. Therefore, main CR usage pertains to staking for resource allocation.
- option 4: Block Producers delegation (Most likely Solution)

## 개발 Roadmap 및 진행 상황 Update 2019.1.2

### There are three phases in developing Burn and Earn 
1. Voting Weight implementation 
- CR coins are transferred to each block producers in determining their BP weight(complete, testing in place)
- Voting weight calculated by months(complete, testing in place)

2. providing dAPP coin according to received CR coins (currently coding)

3. Resource Allocation
- Testing option 4: Block Producers delegation to users (future coding)


