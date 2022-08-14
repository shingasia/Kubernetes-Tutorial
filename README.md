<style type='text/css'>
    #subtitle {
        font-size : 20px;
    }
    #memo {
        font-size : 18px;
    }
</style>
<hr/>
<img src="./images/Kubernetes-Introduction.jpg" />
<hr/>
<p id="subtitle">CNCF(Cloud Native Computing Foundation)은 컨테이너 기술을 발전시키고 기술 산업이 발전할 수 있도록 지원하기 위해 2015년에 설립된 리눅스 재단 소속의 비영리 단체</p>

<p id="subtitle">Google에서 Kubernetes 를 첫 번째 프로젝트로 CNCF에 기증했다.</p>

<p id="subtitle">Cloud Native 애플리케이션의 4가지 구성요소</p>
<ol>
    <li>DevOps<br/>
        DevOps는 Developement와 Operations 를 합친 용어로 소프트웨어를 개발하는 개발자와 이를 운영하는 운영 전문가와의 소통, 협업을 강조하는 문화에서 생겨난 용어이다.
    </li>
    <li>Microservices<br/>
        MSA(Micro Service Architecture)를 통한 서비스 안정성과 스케일링 용이성 개선
    </li>
    <li>Containers<br/>
        컨테이너를 통한 IT 이식성과 유연성 확보
    </li>
    <li>Continuous Delivery(CI/CD)<br/>
        - 지속적 통합 (Continuous Integration)<br/>
        - 지속 배포 CD (Continuous Deployment, Delivery)
    </li>
</ol>
<img src="./images/CNCF-컨테이너.png"/>
<p id="memo">
불변 인프라(Immutable Infrastructure), 지속가능한 인프라스트럭처의 코드화(Infrastructure as Code)와 같은 인프라 패러다임이 가능하도록 하는 데도 많은 기여를 한 것이 컨테이너 기술이다.<br/>
또 많은 컨테이너를 운영하기 위해서는 컨테이너 오케스트레이션 기술이 필요하며, 현재 이 영역에서 사실상(De Facto) 표준으로 통용되고 있는 기술이 바로 <span style="color : #0000ff">'쿠버네티스(Kubernetes)'</span> 이다.<br/>
</p>



