<!-- github-markdown-css -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/5.1.0/github-markdown-dark.css" />
<style type='text/css'>
    .markdown-body {
		box-sizing: border-box;
		/* min-width: 200px;
		max-width: 980px; */
		margin: 0 auto;
		padding: 45px;
	}
	@media (max-width: 767px) {
		.markdown-body {
			padding: 15px;
		}
	}
    .subject1 {
        font-size : 30px;
    }
    .subject2 {
        font-size : 27px;
        color : #80bfff;
    }
    .subtitle {
        font-size : 20px;
        background-color : #b300b3;
        color : #ffffff;
    }
</style>
<div class="markdown-body">
<hr/>
    <p class="subject1">firewalld</p>
<hr/>
<dl>
    <dt><p class="subject2">firewalld에서 사용되는 용어</p><dt>
    <dd><span class="subtitle">1. 런타임(Runtime)</span></dd>
    <dd>
        런타임(실행시간)에만 설정한다는 것이다. 즉, 설정 내역이 메모리에 상주되어 있어 적용은 되지만, firewalld 서비스 중지와 함께 런타임 구성이 손실된다.
        (firewalld를 다시 불러오거나 시스템을 재시작 하면 설정된 내역은 지워지게 된다)
    </dd>
    <dd><span class="subtitle">2. 영구적(Permanent)</span></dd>
    <dd>
        영구적 설정한다는 것이다. (설정파일에 저장되어있다.) <br/>
        즉, <span style="background-color : #4d0099; color : #ffffff; font-size : 16px;">시스템 재시작 또는 서비스 reload/restart 시 새로운 런타임 구성을 설정된 내역에서 불러온다.</span>
        런타임 설정내역을 저장할 수 있는 방법을 제공하지 않기 때문에 영구적 설정으로 관리하는 것이 효율적이다.
    </dd>
    <dd><span style="font-size : 20px;">Runtime to Permanent</span></dd>
    <dd>
        런타임 환경을 사용하여 필요에 맞는 방화벽 설정을 생성할 수 있다. 완료되면 해당 런타임 환경을 영구적으로 마이그레이션 할 수 있다.
        <br/>
        <ul>
            <li><span style="display : inline-block; width : 120px;">firewall-config :</span>Firewalld 방화벽 관리 GUI 프로그램</li>
            <li><span style="display : inline-block; width : 120px;">firewall-cmd :</span>Firewalld 방화벽 관리 CUI 프로그램</li>
        </ul>
    </dd>
    <dd>
        <p style="color : #ff0066; font-size : 16px;">/usr/lib/firewalld 디렉토리에는 icmptypes, 서비스(services) 및 영역(zones)에 대해 firewalld에서 제공하는 기본 및 대체 구성이 포함되어 있습니다.</p>
    </dd>
    <dd><span class="subtitle">3. 영역(Zone)</span></dd>
    <dd>
        방화벽 영역(firewall zone)은 커넥션에 대한 신뢰 순준을 정의한다.<br/>
    </dd>
    <dd>
        <table>
            <caption>Predefined Zones - 기본적으로 정의된 영역</caption>
            <thead>
                <tr>
                    <td>영역(Zone)</td>
                    <td>설명</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>drop</td>
                    <td>
들어오는(incoming) 모든 패킷 <span style="color : #ff0000">폐기(drop)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>block</td>
                    <td>
들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span><br/>
이 시스템 내에서 시작된 네트워크 연결만 가능
                    </td>
                </tr>
                <tr>
                    <td>public</td>
                    <td>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>external</td>
                    <td>
특히 라우터에 대해 마스커레이딩이 활성화된 외부 네트워크에서 사용<br/>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>dmz</td>
                    <td>
DMZ는 비무장지대를 의미한다.<br/>
내부 네트워크에 대한 엑세스가 제한된 조직의 외부 네트워크에 있는 공개적으로 엑세스할 수 있는 컴퓨터를 위한 것.<br/>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>work</td>
                    <td>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>home</td>
                    <td>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>internal</td>
                    <td>
선택한 수신 연결을 제외하고 들어오는(incoming) 모든 패킷 <span style="color : #ff0000">거부(reject)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
                <tr>
                    <td>trusted</td>
                    <td>
들어오는(incoming) 모든 패킷 <span style="color : #0066ff">허용(accept)</span><br/>
나가는(outgoing) 모든 패킷 <span style="color : #0066ff">허용(accept)</span>
                    </td>
                </tr>
            </tbody>
        </table>
    </dd>
    <br/><br/>
    <dd>
        firewall-cmd의 --new-zone, --add-port, --add-service등을 사용하여 서비스, 포트를 직접 추가할 수 있다. 그러나 새 영역(zone)을 정의하고 배포하는 더 빠른 방법은 전용 태그 집합으로 XMl설정파일을 직접 작성하는 것이다.<br/>
        기본 영역(default zones)에 대한 설정파일은 /usr/lib/firewalld/zones 디렉토리에 있다.<br/>
        기본 영역 중 하나가 수정되면 변경 사항이 원래 구성 파일에 직접 기록되지 않는다.<br/>
        대신 /etc/firewalld/zones 디렉토리에 같은 이름의 파일이 생성된다. 이러한 방법으로 만약 영역을 기본 설정으로 리셋하려면, 그냥 해당 파일을 삭제하면 된다.<br/>
    </dd>
    <dd>
        <p style="color : #ff0066; font-size : 16px;">
            기본 영역의 설정을 변경, 또는 사용자 지정 영역(custom zones)을 만들려면  /etc/firewalld/zones 디렉토리에 만들어야 한다
        </p>
    </dd>
    <br/><br/>
    <dd><p>Zone 설정 파일의 기본 구조</p></dd>
    <dd><img src="./network-images/Firewall-Zone-XML.png" /></dd>
    <dd><span class="subtitle">4. 서비스(Service)</span></dd>
    <dd>
        각 서비스별 정의된 프로토콜, 포트, 모듈, 목적지에 대해 정의가 된 서비스이다.<br/>
        여기서 서비스는 /etc/service에 명시된 내용과 다르다.<br/>
        서비스는 service-name.xml 형식으로 명명된 개별 XML구성 파일을 통해 지정된다.
    </dd>
    <br/><br/>
    <dd><p>서비스 XML 파일 예시</p></dd>
    <dd><img src="./network-images/Firewall-Services-XML.png" /></dd>
    <br/><br/>
    <dd><span class="subtitle">5. 마스커레이딩(Masquerading)</span></dd>
    <dd>
        IP 마스커레이딩은 한 대의 컴퓨터가 네트워크의 IP 게이트웨이 역할을 하는 프로세스이다.<br/>
        마스커레이딩에 의해 게이트웨이는 인터페이스 밖으로 나가는 IP를 찾아서 패킷의 source address를 동적으로 이 주소로 바꾼다.<br/>
        마스커레이딩의 일반적인 사용 사례는 라우터가 인터넷에서 라우팅되지 않는 사설 IP 주소를 라우터에서 나가는 인터페이스의 공용 동적 IP 주소로 대체하는 경우이다.
    </dd>
    <br/><br/>
    <dd><span class="subtitle">6. 포트 포워딩(Port Forwarding)</span></dd>
    <dd>
        firewall을 사용하여 시스템의 특정 포트에 도달하는 모든 수신 트래픽이 선택한 다른 내부 포트나 다른 시스템의 외부 포트로 전달되도록 포트 리다이렉션을 설정할 수 있다.
    </dd>
</dl>
</div>
<!--
https://firewalld.org/documentation/zone/
https://firewalld.org/documentation/zone/examples.html
https://www.systutorials.com/docs/linux/man/5-firewalld.zone/ (아주 좋은 문서)
-->

