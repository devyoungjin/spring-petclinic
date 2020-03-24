백기선님의 [예제로 배우는 스프링 입문] 강의를 듣다가 다 듣지못한 적이 있는데, 이번에 다시 듣게되었다. 듣는김에 정리하면 좋을것 같아 정리하면서 작성해보는 글.

[스프링 샘플 웹 애플리케이션](https://github.com/spring-projects/spring-petclinic)을 다뤄보면서 스프링의 IoC, AOP, PSA 등에 대해 예제코드를 통해 맛보는 과정이다.

본 과정은 아래의 조건에 대한 선수학습을 요구한다.

1. 자바 프로그래밍 기초
2. IDE (Intelli J 또는 Eclipse)
3. 빌드 툴 (Gradle 또는 메이븐)
4. Git



## ToC

- 프로젝트 설정
  - [Clone a sample project](#clone)
  - [Build and run a project](#build-run)
- 프로젝트 살펴보기
- 프로젝트 과제

<br>

## <a name="clone">Clone a sample project</a>

먼저 샘플 애플리케이션을 원격저장소에서 클론해서 가져와야 한다. 필자의 경우는 개인 원격저장소로 fork한 이후 clone했다.

원격 저장소의 URI부터 가져오자.

<img src="https://lh3.googleusercontent.com/ov5vKj6r3uJYRU1PAF_Xf_oauZKkRtx5mgWbbte382yTnANwL5mzn5EEBZjyRdITm2crxTtQICW5x4DNht4rC0OFvVvm62um6YhUkfaYsU9C6mI4BkQGUKdzxqWE7dhgEhjPJmFr0y_n76HvyFcr9IZN_UaJqtoJxGpVxCVrVkilWewvBebIw_6V3D3VWtGOKjIl70Upd5jM-GKjhQfcSoyVATyhLzXNTUvzkJd_SvRN4rfN-_s9nZ_8u_jQVk4bOXri33Q9iUrrlf5VrL_2Jh_MbC6cZn8qTIFnsOpRslP8B6aVXG3qjzDe4TgROfNEHz0hm8IMMgLRFMMfXjdpKfqM4Zp2GhGY5dO34ak6iNaEy30ubSGJ3Yrk57J1cBfriVRXiY8cLeplhQfVqiTbPbkcKYY5fnYJEJJPu_snsU4jxzLHx0nfLfyWiRJer4mRYK1ZwGlAfd8nhLK0Y19NhTlWHXbxAOvidYQSltCfL9Wv5DufCtWY4vk0t8p_LWfiFUYnhPFSKuXSJNWaghOU9fXJn46K0VhxYg_SOQqKbuubCKTpD4xaMp9POpvMfGd8cI2uqL8IfPYCZQnYhnSGTAaZOU01jxR0YA22lOFyEd3HDHs1Vh3Du1S6MzkoluGppeRFqusT_ljcXaDPZMCFi812oUoOq8znjjZ99CuebPMGH2j7RSfpZvGekqkOXMc=w987-h592-no" style="zoom:50%;" />



이후에 Intelli J를 열어서 **[Get from Version Control]** 버튼을 클릭하여 아까 클립보드에 복사해둔 원격저장소 URI를 붙여넣어서 가져오자.

![](https://lh3.googleusercontent.com/g40Xf_ZeVVaKzDqAIPPuaQXnGHSj8AsG61l4fiJrme7T1dlAUCJDxnENX1a5SWSpXS3MJgjo4SiYG3EYo6nkyTcJEu83aCwPrQgPBkCj6beFsOZDy5A86rYrXu5HKMKWQ5KM3piuZiLNyz-yWN5aCpe-wwu9kwDI-G59B8fNTaHePWP0v76J_vWaMi3mEvARpLSEZurf7ZK6fn_8Ovl_PGfW747kuzzXMgJ7Jhy4FTT_15MjKDZnyZGmPA2m2KFBJTqGWqLYsXGi_yc2KE2akAc_EYXn7meFvbBor4WMZvIFgNEEA2gNl0oZu05a6SJq7XhzFfe-c4EO6tRGESjoJQLyhqzNCBugGDDNgC1IF6QaRXWSP5GUzWDDw5RLfj71_8_p4xFMqMdqIWkM5_Z3ZBks2Ae2jfL0cXYss0JUpz5wutMtAcYvg0pMDEzMgPMmnTtJlAKVBOsSY8Z-GoWxJ8ZrokwidcFSbxPvd81SxqyRtXbveGH53HxM8c06JmjkuToxDow4_pAXN8GgNnMjcbFtF70ZsoNU5GWb0CMtmKSXTYfdpFlCh301rxhv22rOazKuIjxjBcyMMsAAUW2ROTV7enUlNuIbfBFnb7nVj_q11xWxPFtpftYN2Nunv8JbIv19egBS7WCFISh41cmuCP_9t36k3q6-9QQbGgCAgaeb5GzMc6-ZMeV4iJ8Dv2BbAl2cb-C_shgbvPhlSBRLFI5RUX15mtXpH0-c54mQx_xpWQQdw4QBryDz=w500-h305-no)

<br>

본 샘플 애플리케이션의 빌드 툴은 메이븐이 설정되어 있다. 메이븐의 설정파일 pom.xml을 확인해보면, 따로 `<packaging>`이 설정되어 있지 않은데, 이렇게 따로 `<packaging>`설정이 없으면 이 프로젝트는 jar 프로젝트라고 한다. jar은 Java Application Archive의 약자라고 한다. 타입으로는 war(Web Application Archive)가 있다.



**jar와 war의 차이**

jar는 하나의 java application 기능을 가능하도록 하는 압축파일이며, 자바 클래스 파일들이 주로 압축대상에 해당한다.

war는 jar와 달리 웹 어플리케이션을 지원하기 위한 압축방식인데, jar보다 더 큰 범위의 압축파일이다. 웹 애플리케이션에 필요한 모든 자원(jsp, servlet, gif, html, jar)을 포함한다.

<br>

## <a name="build-run">Build and run a project</a>

당연히 작동되겠지만, 해당 프로젝트가 잘 빌드되고, 작동되는지 알아보자.

**메이븐 빌드하기**

~~~
./mvnw package
~~~

[![asciicast](https://asciinema.org/a/rCuwrlPLzK7FbojYLvqfjGzC4.svg)](https://asciinema.org/a/rCuwrlPLzK7FbojYLvqfjGzC4)

위의 화면처럼 화면 마지막에 <span style="color: green;">**BUILD SUCCESS**</span>가 출력되었다면, 성공적으로 빌드가 된 것이다.

이제 메이븐으로 빌드한 jar파일을 Tomcat(웹 서버)으로 실행해볼 것이다. 

~~~
java -jar target/*jar
~~~

[![asciicast](https://asciinema.org/a/HNNbEegr9IRlpJlydEAfaImOj.svg)](https://asciinema.org/a/HNNbEegr9IRlpJlydEAfaImOj)

<span style="color: green;">**Started PetClinincApplication**</span>이라는 메세지가 마지막에 출력되었다면 성공적으로 실행된 것이다.

로컬호스트에서 정상적으로 프로젝트가 구동되는것을 확인할 수 있다.

![](https://lh3.googleusercontent.com/pT4QlA65nQbcrhP8QvItBOWCRdvfNRXQEnbDy_AUpniXaBFE86V_eK34tJABlMqTCJBSguvolsFfSnvvi5c_GREjUPb2hxmrqLT68yXBFAFD22EZhXQHFZJhrNtdbQGHZVSvNZqDDRBWj2VTZ7f8iYgrSpHZOStNtXhcA3UZUvW7VtaoVV1XVq1KckyI5pFvYpc4F66C7IgISQcuLLOW2FZUSBrULPmyn_EtK3uPuyzkKtlGrgzD7PRp9o8_ipfXjtZkhUJW94Z2ElcJy8e2jnPzLFhhub4PGU111-wXqsAaEWwROtNEzHY7MynutF3VLbpik2HpnMDtniG4l051oJB5EchUSea0qqA5H1ZeQejTXXe2yqLLKhMyt8JG6GGODzCC3dVeikEjWZ4BIUukrQVtOoF5_KsicfL5uVNK1lWcClwja6SgW4MVCXwF4IsfEIEPLeRlYmnwQGxtUcSfeROPKeVwq2wBonT4ihB5bPliyruwt9EWU3b5PF5H2MdDJBwUDtdgWf1d2qYPEyPQaLZSJHZam5e8SAjp3fUwGVe3aRXH4sSiYkORp8Xw3nbQ9UHFx6rMP3Q_mcQ-wvr1puWtrZ_JKHSR3jb9yN0b5Na1PMx5RbrpQ89lh8kR_xnXbdRk4T_eCB-24rRnpubzDQwW4KsPqO00OrUEimPAGuscKREC6sr2n8kz4v1hkginOx85h67dklGvZZ46m49FJtIjOcB_qzQL_xGlz83MBBfB48apa3D5dSyA=w1440-h922-no)

<br>

## 